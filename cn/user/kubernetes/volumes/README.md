# 卷

在 Kubernetes 中，卷是可供应用程序使用的文件系统的抽象。在 Portainer 中，您可以管理集群中由应用程序部署的卷。

也可以通过点击**从清单创建**来[使用清单](../applications/manifest.md)添加卷。

[inspect.md](inspect.md)

[remove.md](../../docker/volumes/remove.md)

## 卷标签页

让您可以查看集群中存在的卷的信息，包括：

* 每个卷所属的命名空间。
* 哪些应用程序使用每个卷。
* 每个卷所属的存储类。
* 每个卷的大小。
* 卷的创建时间和创建者。
* 带有**external**标志的卷是在 Portainer 外部创建的，这意味着与在 Portainer 内部创建的卷相比，Portainer 对其了解有限。**unused**标签表示 Portainer 看不到任何使用此卷的应用程序。由于可用信息有限，此标签也可能出现在**external**资源上。

<figure><img src="../..//assets/2.15-kubernetes_volumes_voulme_list.png" alt=""><figcaption></figcaption></figure>

## 存储标签页

存储标签页列出了基础设施中可用的存储类以及每个卷使用的磁盘空间。每个存储类可以展开以列出其中包含的卷。

<figure><img src="../..//assets/2.15-kubernetes_volumes_storage_list.png" alt=""><figcaption></figcaption></figure>
