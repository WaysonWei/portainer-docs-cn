# 浏览注册表

注册表管理器通过让您能够浏览已定义的注册表并操作其内容，扩展了您的容器管理体验。使用此功能，容器用户可以享受单一界面管理任何Docker注册表部署的优势，提供跨任何提供商的一致外观和感觉。

您的注册表必须支持Docker Registry API v2才能与Portainer集成。

从菜单中选择**注册表**，然后选择要浏览的注册表旁边的**浏览**。

<figure><img src="..//assets/2.15-registries-browse.gif" alt=""><figcaption></figcaption></figure>

将显示注册表中的存储库列表以及每个存储库的标签数量。选择一个存储库以查看其详细信息。

<figure><img src="..//assets/2.15-registries-browse-repos.png" alt=""><figcaption></figcaption></figure>

**存储库信息**页面提供存储库名称、标签和镜像计数，以及所有标签的列表。您可以重新标记镜像以通过部署生命周期提升它，或者简单地添加或删除标签来注释更改或使用情况。

此页面还提供了一个选项，通过安全删除未使用的旧镜像来清理它们。您还可以删除整个存储库。

<figure><img src="..//assets/2.15-registries-browse-repo-detail.png" alt=""><figcaption></figcaption></figure>
