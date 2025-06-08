# ConfigMaps & Secrets

在Portainer中，您可以在服务镜像或运行容器之外创建配置。这使您能够保持镜像尽可能通用，无需将配置文件绑定挂载到容器中或使用环境变量。

此部分以前称为**配置**。

本页面分为两个标签页 - [ConfigMaps](./#configmaps) 和 [Secrets](./#secrets)。

## ConfigMaps

此标签页显示Kubernetes集群中存在的ConfigMaps。默认情况下，系统资源是隐藏的。要查看它们，点击右侧的三点菜单并勾选**显示系统资源**。

<figure><img src="../..//assets/2.19-kubernetes-configurations-configmaps-list.png" alt=""><figcaption></figcaption></figure>

您可以通过点击**筛选**并勾选要查看的命名空间来按命名空间筛选ConfigMaps的显示。

带有**external**标志的ConfigMap是在Portainer外部创建的，这意味着Portainer对其了解有限，与在Portainer内创建的ConfigMap相比。**unused**标签表示Portainer看不到任何使用此ConfigMap的应用程序。由于可用信息有限，此标签也可能出现在**external**资源上。

要通过表单添加新的ConfigMap，点击**使用表单添加**按钮。要通过manifest添加，点击**从manifest创建**。

[add.md](add.md)

要移除ConfigMap，勾选要移除的ConfigMap旁边的复选框，然后点击**移除**按钮。

## Secrets

此标签页显示Kubernetes集群中存在的secrets。默认情况下，系统资源是隐藏的。要查看它们，点击右侧的三点菜单并勾选**显示系统资源**。

<figure><img src="../..//assets/2.19-kubernetes-configurations-secrets-list.png" alt=""><figcaption></figcaption></figure>

您可以通过点击**筛选**并勾选要查看的命名空间来按命名空间筛选secrets的显示。

带有**external**标志的secret是在Portainer外部创建的，这意味着Portainer对其了解有限，与在Portainer内创建的secret相比。**unused**标签表示Portainer看不到任何使用此secret的应用程序。由于可用信息有限，此标签也可能出现在**external**资源上。

要通过表单添加新的secret，点击**使用表单添加**按钮。要通过manifest添加，点击**从manifest创建**。

[add-1.md](add-1.md)

要移除secret，勾选要移除的secret旁边的复选框，然后点击**移除**按钮。
