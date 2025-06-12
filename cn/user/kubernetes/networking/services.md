# Services

在 Kubernetes 中，**Service** 是一种用于将应用程序（运行在 pods 中）暴露到网络的对象。

Services 页面列出了集群中的服务，并提供每个服务的详细信息。要查看服务列表，请展开左侧菜单中的 **Networking** 并选择 **Services**。

<figure><img src="../..//assets/2.20-kubernetes-networking-services.gif" alt=""><figcaption></figcaption></figure>

用户有权访问的所有服务都列在此页面上。

<figure><img src="../..//assets/2.20-kubernetes-networking-services-list.png" alt=""><figcaption></figcaption></figure>

对于每个服务，列表会显示服务的 **名称**、所属的 **应用** 和 **命名空间**、服务 **类型**、暴露的 **端口** 和 **目标端口**、**集群 IP** 和 **外部 IP**（如果有）以及 **创建日期** 和 **用户**（如果可用）。在 Portainer 外部配置的服务会标记为 **external** 标签，系统服务会标记为 **system** 标签。

系统服务的显示可以在表格设置中切换（点击表格右上角的三个点并勾选 **Show system resources**）。
