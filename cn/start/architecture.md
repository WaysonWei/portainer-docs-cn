# Portainer架构

## Portainer架构概述

Portainer由两个组件组成：Portainer Server和Portainer Agent。两者都作为轻量级容器运行在您现有的容器化基础设施上。Portainer Agent应部署到集群中的每个节点，并配置为向Portainer Server容器报告。

要深入了解Portainer架构，请查看我们的[参考架构](https://academy.portainer.io/architecture)。

单个Portainer Server可以接受来自任意数量Portainer Agent的连接，从而提供从一个集中界面管理多个集群的能力。为此，Portainer Server容器需要数据持久化。Portainer Agent是无状态的，数据会被传送回Portainer Server容器。

![Portainer架构](/assets/portainer-architecture-detailed.png)

我们目前不支持运行多个Portainer Server容器实例来管理相同的集群。我们建议在特定的管理节点上运行Portainer Server，并在其余节点上部署Portainer Agent。

## Agent与Edge Agent对比

在标准部署中，中央Portainer Server实例及其管理的任何环境都假定在同一网络上，即Portainer Server和Portainer Agent能够无缝通信。然而，在远程环境与Portainer Server完全分离的网络配置中（例如通过互联网），传统上我们将无法集中管理这些设备。

通过新的Edge Agent，我们改变了架构。Portainer Server不再需要无缝访问远程环境，而是只需要远程环境能够访问Portainer Server。这种通信通过加密的TLS隧道进行。这对于不希望将Portainer Agent暴露在互联网上的互联网连接配置非常重要。

## 安全与合规

Portainer完全在您的服务器上、您的网络内、您的防火墙后运行。因此，我们目前不持有任何SOC或PCI/DSS合规认证，因为我们不托管您的任何基础设施。您甚至可以完全断开连接（物理隔离）运行Portainer，而不会影响功能。

虽然我们（可选地）会从Portainer安装中收集匿名使用分析数据，但我们始终符合GDPR要求。数据收集可以在安装产品时或之后的任何时间禁用。如果您的安装是物理隔离的，收集将静默失败而不会产生任何不良影响。

[lifecycle.md](lifecycle.md)
