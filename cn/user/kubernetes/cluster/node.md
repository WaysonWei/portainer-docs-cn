# 检查节点

要查看集群中单个节点的详细信息，从菜单展开**集群**并选择**详情**，然后向下滚动并点击要检查的节点名称。

<figure><img src="../..//assets/2.20-kubernetes-cluster-node-inspect.gif" alt=""><figcaption></figcaption></figure>

关于集群的信息分为两个屏幕标签页。

## 节点

**节点**标签页总结了所选节点的以下信息：

| 字段/选项    | 概述                                                                               |
| ------------ | ---------------------------------------------------------------------------------- |
| 主机名       | 节点的主机名。                                                                     |
| Kubernetes API | 该节点的Kubernetes API地址和端口。                                                 |
| 角色         | 节点的角色。                                                                       |
| Kubelet版本  | 节点上的kubelet版本。                                                              |
| 创建日期     | 该节点的创建日期。                                                                 |
| 状态         | 节点的状态。                                                                       |
| 可用性       | 定义节点的可用性。选项为**活动**、**暂停**和**排空**。                             |

<figure><img src="../..//assets/2.15-k8s-cluster-node-details.png" alt=""><figcaption></figcaption></figure>

### 资源预留

此部分提供有关节点上分配的资源预留以及节点资源使用情况的详细信息。

**内存使用**和**CPU使用**仅在[启用了指标API](setup.md#enable-features-using-metrics-server)时显示。

<figure><img src="../..//assets/2.15-k8s-cluster-node-resource.png" alt=""><figcaption></figcaption></figure>

### 标签

此部分列出应用于节点的标签。如果需要，可以添加其他标签，以及编辑非系统标签。

<figure><img src="../..//assets/2.15-k8s-cluster-node-labels.png" alt=""><figcaption></figcaption></figure>

### 污点

在此部分可以添加污点以防止某些Pod部署在节点上。

<figure><img src="../..//assets/2.15-k8s-cluster-node-taints.png" alt=""><figcaption></figcaption></figure>

## 事件

显示与节点相关的事件信息。

<figure><img src="../..//assets/2.15-k8s-cluster-node-events.png" alt=""><figcaption></figcaption></figure>

## 在此节点上运行的应用程序

此部分提供有关所选节点上运行的应用程序的信息。点击应用程序名称将转到该应用程序的详细信息页面。

<figure><img src="../..//assets/2.15-k8s-cluster-node-apps.png" alt=""><figcaption></figcaption></figure>
