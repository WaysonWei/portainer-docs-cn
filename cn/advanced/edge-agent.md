# Portainer Edge Agent

## 背景故事

对于标准部署，我们过去假设Portainer实例和所有环境共享同一网络并能无缝通信。如果远程环境位于不同网络（例如通过互联网），我们就无法管理它们。

后来我们改变了Edge Agent架构，现在只需要环境能够访问Portainer。不再需要将Portainer Agent暴露在互联网上。

Portainer现在只需要开放`9443`和`8000` TCP端口。我们过去从`9000`端口提供UI和Portainer API，但现在扩展了API以允许远程Agent轮询指令。端口`8000`是一个TLS隧道服务器，用于在Agent和Portainer实例之间创建安全隧道。更多细节将在后面介绍。

如果Portainer实例部署时启用了TLS，Agent将使用HTTPS连接回Portainer。但如果您的Portainer实例使用自签名证书，则必须使用`-e EDGE_INSECURE_POLL=1`标志部署Edge Agent。如果不使用此标志部署Edge Agent，Agent将无法与Portainer实例通信。

## 在Portainer中创建Edge Agent

创建Edge Agent时，首先需要为环境指定一个易于理解的名称。然后需要确认Portainer实例的FQDN:PORT。这是Agent用来连接的地址，请确保其正确且DNS可解析。

在创建过程中，会动态生成一个Edge ID。这是一个随机UUID，分配给每个环境。您可以在设置过程中提供的命令语法中看到它。

<figure><img src="/assets/2.15-advanced-edgeagent-command.png" alt=""><figcaption></figcaption></figure>

Edge ID和加入令牌(join token)对每个环境都是唯一的。加入令牌(`EDGE_KEY`)由以下base64编码数据组成，用竖线(`|`)分隔：

* Portainer实例API URL。这是Edge Agent知道如何"回拨"到您的Portainer实例的方式。
* Portainer实例反向隧道服务器地址。这与API URL相同（除非在[部署过程中更改](../admin/environments/add/docker/edge.md#deploying)或在[边缘计算设置](../admin/settings/edge.md#edge-compute-settings)中修改），但使用隧道服务器端口（默认为`8000`）。
* Portainer实例反向隧道服务器指纹（防止创建隧道时的中间人攻击）。
* 环境标识符键（端点/环境ID）。

使用命令语法在远程节点或远程Swarm集群上部署Edge Agent。

## Portainer和Edge Agent如何通信

### 轮询

Agent默认每5秒轮询Portainer实例一次（这在Portainer设置中定义）。

### 连接过程和检查

Agent向Portainer说："嗨，我是一个Agent。我的加入令牌是`abc123`。你现在需要我吗？"。Portainer检查其数据库以确保Edge UUID和加入令牌匹配。如果没有UUID能与提供的加入令牌关联，Portainer会将Agent提供的UUID与环境加入令牌关联。

如果UUID/加入令牌不匹配，连接将被拒绝。如果匹配，Portainer实例会响应："不，我不需要你。请在X秒后再检查。"（X是Agent轮询频率），或者"是的，我需要你。请使用这些隧道凭证连接。"

Portainer使用Edge UUID作为加密密钥加密隧道凭证（设计为一次性使用凭证）。

### 在Agent和Portainer之间打开隧道

一旦收到确认，Edge Agent解密凭证并在端口`8000`上打开到Portainer实例的隧道。如果远程环境是Swarm集群，每个节点都将运行一个Agent实例（每个实例都会轮询Portainer）。"你需要"标志会导致集群中的第一个Agent建立隧道。一旦建立，Portainer就可以查询隧道开放的Agent。如果隧道因任何原因关闭，Agent会立即重新建立它。

### 当Portainer强制Edge Agent建立隧道时

有时Portainer会要求Agent建立隧道。这发生在管理员通过Portainer UI或API选择Edge环境进行交互式管理时。一旦选择，"你需要"标志会触发连接过程。如果使用默认设置，Agent轮询并建立隧道大约需要10秒。大约5秒等待轮询，然后几秒钟打开隧道。在此过程中管理员会看到此消息：

<div align="center"><img src="/assets/edge-advanced-2.png" alt=""></div>

### 终止连接

Agent记录Portainer上次与其通信的时间。5分钟不活动后，它会将当前配置的快照发送给Portainer记录，关闭隧道并撤销凭证。当管理员与Edge环境有活动会话时，即使管理员没有执行任务，也会每分钟发送"保持活动"信号，以免被错误踢出。

## 网络性能

### 调整轮询频率以提高性能

数千个端点每5秒轮询Portainer一次是很大的负载。这大约是每个Agent 324b/秒，不是每个环境。如果您不经常进行环境管理，我们建议您进入Portainer设置并增加轮询频率。只需在需要管理时将其改回，这样您就不必等待。

<figure><img src="/assets/2.15-advanced-edgeagent-pollfreq.png" alt=""><figcaption></figcaption></figure>

### 持续改进

我们使用15,000个活动连接的环境和5秒的轮询频率对Portainer进行了负载测试。这向Portainer实例生成了7Mbps的网络流量，Portainer需要4个CPU来处理加密/隧道负载。这个Edge Agent版本是我们首次尝试大规模集中管理。我们的最终目标是减少与轮询相关的网络开销。
