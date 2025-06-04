# 管理注册表

注册表管理器通过让您能够浏览已定义的注册表并操作其内容，扩展了您的容器管理体验。使用此功能，容器用户可以享受单一界面管理任何Docker注册表部署的优势，提供跨任何提供商的一致外观和感觉。

## 添加标签

从菜单中选择**注册表**，选择要管理的注册表，然后点击**浏览**。从列表中选择要管理的存储库。

<figure><img src="..//assets/2.15-registries-manage.gif" alt=""><figcaption></figcaption></figure>

在页面右上角的**添加标签**部分，输入标签名称，从下拉菜单中选择镜像，然后点击**添加标签**按钮。

<figure><img src="..//assets/2.15-registries-manage-addtag.png" alt=""><figcaption></figcaption></figure>

## 重新标记

如果您托管自己的Docker注册表，并且想要重新标记镜像的能力，您需要将以下内容添加到Docker注册表的环境变量中：

`REGISTRY_STORAGE_DELETE_ENABLED=TRUE`

从菜单中选择**注册表**，选择要管理的注册表并点击**浏览**。从存储库列表中，选择要管理的存储库。

<figure><img src="..//assets/2.15-registries-manage.gif" alt=""><figcaption></figcaption></figure>

在**标签**部分，找到要重新标记的镜像，然后点击其右侧的**重新标记**。输入镜像的新标签，然后点击勾选图标。

<figure><img src="..//assets/2.15-registries-manage-retag.png" alt=""><figcaption></figcaption></figure>

## 移除标签

如果您托管自己的Docker注册表，并且想要移除标签的能力，您需要将以下内容添加到Docker注册表的环境变量中：

`REGISTRY_STORAGE_DELETE_ENABLED=TRUE`

从菜单中选择**注册表**，选择要管理的注册表，然后点击**浏览**。从列表中选择要管理的存储库。

<figure><img src="..//assets/2.15-registries-manage.gif" alt=""><figcaption></figcaption></figure>

勾选要移除的标签旁边的复选框，然后点击**移除**。

<figure><img src="..//assets/2.15-registries-manage-removetag.gif" alt=""><figcaption></figcaption></figure>

当确认消息出现时，如果确定，点击**移除**。
