# 注册表

注册表是容器镜像的存储库，可以拉取并部署在容器化基础设施上。Portainer支持将注册表连接到Portainer Server实例，允许您在部署容器时使用这些注册表。

<figure><img src="..//assets/2.15-admin-registries.png" alt=""><figcaption></figcaption></figure>

[添加注册表](add/)

[自定义注册表](add/custom.md)

使用Portainer商业版，您还可以在Portainer内部浏览和管理您的注册表。

[浏览注册表](browse.md)

[管理注册表](manage.md)

## 隐藏匿名Docker Hub

默认情况下，**Docker Hub(匿名)**注册表对所有用户可用。如果您希望从注册表选择中隐藏它，可以点击**为所有用户隐藏**。

<figure><img src="..//assets/2.15-admin-registries-dockerhub-hide.png" alt=""><figcaption></figcaption></figure>

由于匿名Docker Hub访问内置于Docker本身，这不会完全禁用对此注册表的访问，但会将其从Portainer UI的注册表下拉列表中隐藏。此外，如果没有其他注册表可供用户使用，无论此设置如何，Docker Hub(匿名)选项都将显示。
