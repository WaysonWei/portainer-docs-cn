# 在Docker Swarm上安装Portainer Agent

Portainer使用_Portainer Agent_容器与_Portainer Server_实例通信并提供对节点资源的访问。本文档将介绍如何在环境中安装Portainer Agent以及如何从Portainer Server实例连接到它。如果您还没有可用的Portainer Server实例，请先参考[Portainer Server安装指南](../../../../start/install/server/swarm/linux.md)。

除了Docker Swarm环境的通用要求外，您还需要：

* 管理节点和工作节点必须能够通过端口`9001`相互通信。此外，Portainer Server安装必须能够通过端口`9001`访问节点。如果无法实现，我们建议考虑使用[Edge Agent](edge.md)。
* 如果您的节点运行Windows，则需要：
  * 安装Windows Subsystem for Linux (WSL)并选择Linux发行版。对于新安装，我们推荐WSL2。
  * 配置并运行Windows Container Services (WCS)。

Portainer Agent安装说明还对您的环境做出以下额外假设：

* 运行Docker的机器上已禁用SELinux。
* 您通过Unix sockets（或使用WCS时的命名管道）访问Docker。
* 您没有在Portainer Server实例上设置自定义`AGENT_SECRET`。如果设置了（通过在启动Portainer Server容器时指定`AGENT_SECRET`环境变量），部署时需要以相同方式（作为环境变量）向您的agent提供相同的密钥，例如在stack文件中添加：

    `environment:`

    &#x20; `- AGENT_SECRET: yoursecret`

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

接下来，选择**Docker Swarm**作为环境类型，然后点击**开始向导**。选择**Agent**选项和您的平台。复制命令，然后在Docker Swarm集群的管理节点上运行。例如，如果您在Linux机器或安装了WSL的Windows机器上部署，请使用**Linux & Windows WSL**命令。如果您在安装了WCS的Windows机器上部署，请使用**Windows WCS**命令。

在输入环境详细信息之前，必须在Docker Swarm集群上运行该命令。

如果要使用Portainer Agent的[主机管理功能](../../../../user/docker/swarm/setup.md#host-and-filesystem)，应向Portainer提供的命令添加必要的卷挂载：

```
--mount type=bind,src=//,dst=/host
```

如果要部署Agent的环境上的Docker卷路径位于非标准位置（而不是`/var/lib/docker/volumes`），则需要调整部署命令中的卷挂载以适应。

例如，如果您的卷路径是`/srv/data/docker`，您需要将命令中的行更改为：

```
--mount type=bind,src=//srv/data/docker,dst=/var/lib/docker/volumes \
```

挂载的`dst`值应保持为`/var/lib/docker/volumes`，因为这是Agent期望的。

<figure><img src="../../..//assets/2.16-environments-add-swarm-agent.png" alt=""><figcaption></figcaption></figure>

部署命令将返回类似以下内容：

```
Creating network portainer-agent_portainer_agent
Creating service portainer-agent_agent
```

要验证agent是否正在运行，请运行以下命令：

```
 docker service ls
```

结果应如下所示：

```
ID                  NAME                    MODE                REPLICAS            IMAGE                    PORTS
tshb6ee2710s        portainer-agent_agent   global              1/1                 portainer/agent:latest
```

无论集群中有多少个节点，只需为您的环境执行此操作**一次**。您**不需要**将每个节点作为单独的环境添加到Portainer中。只需添加一个节点（我们推荐管理节点）即可让Portainer管理整个集群。

一旦agent在Docker Swarm集群上运行，请参考下表输入环境详细信息：

<table><thead><tr><th width="238">字段</th><th>概述</th></tr></thead><tbody><tr><td>名称</td><td>为环境指定一个描述性名称。</td></tr><tr><td>环境地址</td><td>输入Portainer Server实例可以访问环境的IP或DNS名称以及端口(<code>9001</code>)。</td></tr></tbody></table>

<figure><img src="../../..//assets/2.15-environments-add-swarm-agent-config.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分，通过将环境添加到[组](../../groups.md)或[标记](../../tags.md)来分类环境以提高可搜索性。

<figure><img src="../../..//assets/2.18-environments-add-docker-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
