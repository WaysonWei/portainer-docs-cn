# 镜像仓库

**镜像仓库**功能让您可以管理对当前可用仓库的访问。

此处分配的仓库访问权限仅适用于所选环境，不是全局的。

## 添加新仓库

从菜单展开**集群**，选择**镜像仓库**然后点击**添加仓库**。当全局仓库页面出现时，按照[这些说明](../../../admin/registries/add/)操作。

<figure><img src="../..//assets/2.15-k8s-cluster-registries-add.gif" alt=""><figcaption></figcaption></figure>

## 管理访问权限

要配置对仓库的访问权限，从菜单展开**集群**然后选择**镜像仓库**。

<figure><img src="../..//assets/2.15-k8s-cluster-registries.gif" alt=""><figcaption></figcaption></figure>

找到您要管理的仓库然后选择**管理访问**。

<figure><img src="../..//assets/2.15-k8s-cluster-registries-manage.png" alt=""><figcaption></figcaption></figure>

从下拉菜单中选择您希望授予访问权限的命名空间，然后点击**创建访问**。

<figure><img src="../..//assets/2.15-k8s-cluster-registries-createaccess.png" alt=""><figcaption></figcaption></figure>

您可以在**访问**部分查看具有仓库访问权限的命名空间列表，或移除命名空间对仓库的访问权限。

<figure><img src="../..//assets/2.15-k8s-cluster-registries-access.png" alt=""><figcaption></figcaption></figure>

## 浏览仓库

仓库管理器扩展了您的容器管理体验，使您能够浏览已定义的仓库并操作其内容。通过此功能，容器用户可以享受单一界面管理任何Docker仓库部署的优势，提供跨任何提供商的一致外观和体验。

您的仓库必须支持Docker Registry API v2才能与Portainer集成。

选择您要浏览的仓库旁边的**浏览**。

将显示仓库内的存储库列表以及每个存储库的标签数量。选择一个存储库以查看其详细信息。

<figure><img src="../..//assets/2.15-k8s-cluster-registries-browse.png" alt=""><figcaption></figcaption></figure>

**存储库信息**页面提供存储库名称、标签和镜像计数，以及所有标签的列表。您可以重新标记镜像以通过部署生命周期提升它，或者简单地添加或删除标签以注释更改或使用情况。

此页面还提供了通过安全删除来清理未使用的旧镜像的选项。您也可以删除整个存储库。

您可以在仓库上执行的操作可能会受到用户角色的限制。

<figure><img src="../..//assets/2.15-registries-browse-repo-detail.png" alt=""><figcaption></figcaption></figure>
