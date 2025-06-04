# 添加Docker Swarm环境

Portainer支持通过多种方式连接到Docker Swarm环境。根据您的需求选择最适合的方法：

* **Agent** - 推荐用于大多数情况。Portainer Agent作为容器运行在您的Swarm管理节点上，提供完整的Portainer功能集。
* **API** - 直接连接到Docker API，无需部署Agent。
* **Socket** - 直接连接到Docker socket，适用于本地环境。
* **Edge Agent标准** - 当远程环境无法直接从Portainer Server实例访问时使用。
* **Edge Agent异步** - 类似于标准Edge Agent，但使用消息队列系统进行通信，适用于高延迟或不可靠网络连接。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

## 选择连接方法

选择最适合您需求的连接方法：

| 方法 | 优点 | 缺点 |
|------|------|------|
| **Agent** | 完整功能支持<br>实时通信<br>最佳性能 | 需要在集群上部署Agent |
| **API** | 无需部署Agent<br>快速设置 | 功能有限<br>需要网络连通性 |
| **Socket** | 本地连接<br>无需网络配置 | 仅适用于本地环境 |
| **Edge Agent标准** | 无需开放入站端口<br>适用于受限网络 | 轮询延迟 |
| **Edge Agent异步** | 适用于高延迟网络<br>更可靠通信 | 需要额外基础设施 |

## 开始之前

* 确保您的Docker Swarm环境满足[系统要求](../../../../start/requirements-and-prerequisites.md)
* 对于Agent连接，确保网络允许Portainer Server与Docker API通信
* 对于Edge Agent，确保防火墙允许访问Portainer Server的UI端口(9443)和隧道端口(8000)

## 后续步骤

根据您选择的连接方法，继续阅读相应的文档：

* [使用Agent连接](agent.md)
* [使用API连接](api.md)
* [使用Socket连接](socket.md)
* [使用Edge Agent标准连接](edge.md)
* [使用Edge Agent异步连接](edge-async.md)
