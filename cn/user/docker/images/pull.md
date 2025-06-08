# 拉取镜像

您可以从任何[已添加到Portainer](../../../admin/registries/)的注册表拉取镜像，或者使用高级模式从自定义外部注册表拉取。

在多节点环境中，拉取的镜像仅会出现在您在**部署**部分选择的节点上。要使镜像对所有节点可用，请考虑[添加注册表](../../../admin/registries/add/)到Portainer。

## 方法1：简单模式拉取镜像

此方法允许您从Docker Hub或之前连接过的其他注册表拉取镜像。

从菜单中选择**镜像**。选择要使用的注册表然后输入镜像名称。在多节点环境中，选择要部署到的节点。

<figure><img src="../..//assets/2.15-docker_images_pull_images (1).png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**拉取镜像**。

## 方法2：高级模式拉取镜像

使用高级模式，您可以定义自定义注册表URL、端口和镜像。如果您运行自己的私有注册表但不想将其添加到Portainer的[注册表](../../../admin/registries/)列表中，这非常理想。

从菜单中选择**镜像**然后选择**高级模式**。接下来，在**镜像**框中输入注册表、端口和镜像。在多节点环境中，选择要部署到的节点。

<figure><img src="../..//assets/2.15-docker_images_pull_image_simple.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**拉取镜像**。
