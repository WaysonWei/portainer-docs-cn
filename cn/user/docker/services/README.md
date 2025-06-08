# 服务

**服务**菜单仅适用于Docker Swarm端点。

服务包含镜像定义、容器配置以及这些容器如何在Swarm集群中部署的指令。

<figure><img src="../..//assets/2.20-services-list.png" alt=""><figcaption></figcaption></figure>

当启用[新镜像指示器](../swarm/setup.md#other)功能时，**镜像最新**列会显示服务中的本地镜像是否为最新版本，绿色勾表示是最新版本，橙色叉表示远程注册表中有更新的镜像版本。灰色连字符表示Portainer无法确定镜像是否有可用更新。

您可以点击**重新加载镜像指示器**按钮重新检查所有服务的镜像更新，或者点击单个服务的镜像指示器图标重新检查该服务的镜像。

有关工作原理的更多信息，请参阅[此知识库文章](https://portal.portainer.io/knowledge/how-does-the-image-update-notification-icon-work)。

[add.md](add.md)

[configure.md](configure.md)

创建服务后，您可以扩展它以满足需求，并查看单个任务状态和日志。

[scale.md](scale.md)

[tasks.md](tasks.md)

[logs.md](logs.md)

如果需要撤销对服务的某些更改，您可以回滚它。

[rollback.md](rollback.md)

您还可以为服务配置webhooks。

[webhooks.md](webhooks.md)
