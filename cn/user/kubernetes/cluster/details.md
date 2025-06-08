# 集群详情

集群是运行容器化工作负载的节点集合。Portainer让您可以跟踪集群及其各个节点，包括资源使用情况和配置。

从菜单展开**集群**部分并选择**详情**。

<figure><img src="../..//assets/2.20-kubernetes-cluster-details.gif" alt=""><figcaption></figcaption></figure>

提供以下信息：

| 属性          | 概述                                                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 内存预留      | 集群可用的内存量。                                                                                                                                    |
| 内存使用      | 集群使用的内存量。仅在[启用了指标API](setup.md#enable-features-using-the-metrics-api)时可见。                                                         |
| CPU预留       | 集群中已预留的CPU量。                                                                                                                                 |
| CPU使用       | 集群使用的CPU量。仅在[启用了指标API](setup.md#enable-features-using-the-metrics-api)时可见。                                                          |

<figure><img src="../..//assets/2.27-kubernetes-cluster-details-resource-reservation.png" alt=""><figcaption></figcaption></figure>

## Omni集群管理

此部分仅当环境是通过Omni[由Portainer配置的Talos Kubernetes集群](../../../admin/environments/add/kube-create/omni.md)时出现。

在此部分，您可以查看和更新由Portainer通过Omni配置的Talos Kubernetes集群上的Kubernetes和Talos版本。

此功能处于测试阶段，仅测试了部分配置。

<figure><img src="../..//assets/2.26-kubernetes-cluster-details-omni.png" alt=""><figcaption></figcaption></figure>

## MicroK8s集群管理

此部分仅当环境是通过[创建Kubernetes集群](../../../admin/environments/add/kube-create/microk8s/)功能配置的MicroK8s集群时出现。

在此部分，您可以查看和更改由Portainer配置的MicroK8s集群的配置。

此功能处于测试阶段，仅测试了部分配置。有关使用此功能的注意事项，请参阅我们的[已知问题知识库文章](https://portal.portainer.io/knowledge/microk8s-known-issues)。

| 字段/选项                        | 概述                                                                                                                                                                                                                                                                                                                    |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Kubernetes版本                  | <p>显示集群上运行的Kubernetes版本。<br>如果有新版本的Kubernetes可用，您可以点击<strong>升级</strong>按钮将集群升级到指定版本。注意升级过程中可能会导致集群暂时不可用。</p> |
| 必需插件(已安装) | 显示集群上已安装的必需插件列表。                                                                                                                                                                                                                                                  |
| 可选插件                     | 显示集群上安装的可选插件(如果有)以及配置中使用的任何参数。您可以在此调整插件的参数，点击**添加插件**按钮添加其他插件，或点击插件旁边的垃圾桶图标移除插件。             |

<figure><img src="../..//assets/2.19-kubernetes-cluster-microk8s.png" alt=""><figcaption></figcaption></figure>

点击**应用更改**按钮应用对插件配置的任何调整，或点击**取消**恢复更改。

## 节点

此部分列出集群中的节点及其相关信息。要查看[特定节点的详情](node.md)，点击列表中节点的名称。

<figure><img src="../..//assets/2.27-kubernetes-details-nodes-list.png" alt=""><figcaption></figcaption></figure>

**状态**列显示节点上当前活动的任何状态。如果没有显示状态，则表示节点健康。任何活动状态(DiskPressure、MemoryPressure、PIDPressure、NetworkUnavailable)都会显示在相应节点上。

要查看节点的使用统计信息，点击节点右侧的统计图标。

节点统计信息仅在[启用了指标API](setup.md#enable-features-using-the-metrics-api)时可用。

<figure><img src="../..//assets/2.17-k8s-cluster-nodestats.png" alt=""><figcaption></figcaption></figure>

在使用[创建Kubernetes集群](../../../admin/environments/add/kube-create/)功能配置的Talos Kubernetes或MicroK8s环境中，您还将看到添加和移除节点的按钮，以及在MicroK8s环境上查看MicroK8s状态(控制平面节点)和通过SSH控制台连接到环境的额外操作图标。

如果需要调整Kubernetes配置的元素，可以通过在左侧菜单中选择**设置**来完成。

[setup.md](setup.md)

如果想在环境中定义Pod的安全约束，选择**安全约束**。

[security.md](security.md)
