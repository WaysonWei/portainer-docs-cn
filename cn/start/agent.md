# 添加环境到现有安装

Portainer Agent 是一个轻量级的 Docker 容器，可以在现有的 Docker 或 Kubernetes 环境中运行，使 Portainer Server 能够管理该环境。

## 为什么使用 Portainer Agent?

Portainer Agent 提供了几个关键优势：

1. **更安全的通信** - Agent 使用 TLS 加密与 Portainer Server 的所有通信
2. **减少防火墙配置** - 只需要从 Agent 到 Server 的出站连接
3. **更好的性能** - Agent 在本地处理操作，减少网络延迟
4. **集群支持** - 在 Swarm 或 Kubernetes 集群中的每个节点上部署 Agent 以实现完整管理

## 部署 Portainer Agent

要在现有环境中部署 Portainer Agent：

1. 在 Portainer UI 中导航到 **Environments** 页面
2. 点击 **Add environment**
3. 选择环境类型 (Docker, Kubernetes 等)
4. 按照显示的说明在目标环境中部署 Agent
5. 完成后，新环境将出现在您的环境列表中

[了解更多关于 Portainer Agent 架构的信息](../advanced/edge-agent.md)
