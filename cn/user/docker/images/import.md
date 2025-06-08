# 导入镜像

您可以从其他Portainer实例、Docker CLI或Docker Swarm CLI导入镜像。

从菜单中选择**镜像**，然后点击**导入**。

<figure><img src="../..//assets/2.15-docker_images_build_image_import.gif" alt=""><figcaption></figcaption></figure>

点击**选择文件**浏览要上传的镜像文件。Portainer支持`.tar`、`.tar.gz`、`.tar.bz2`和`.tar.xz`文件。如果在多节点环境中，选择要保存镜像的节点。

在多节点环境中，导入的镜像仅会出现在**部署**下选择的节点上。如果希望镜像对所有节点可用，请考虑[添加注册表](../../../admin/registries/add/)到Portainer。

<figure><img src="../..//assets/2.15-docker_images_upload_file.png" alt=""><figcaption></figcaption></figure>

导入镜像时，您还可以选择使用Portainer中预配置的注册表标记镜像。从下拉菜单中选择**注册表**并输入镜像名称和标签。

<figure><img src="../..//assets/2.15-docker_images_upload_file_tag_image.png" alt=""><figcaption></figcaption></figure>

如果希望使用Portainer中未配置的注册表标记镜像，点击**高级模式**并根据需要输入注册表、端口、镜像和标签。

如果希望在本地而非注册表中标记镜像，使用**高级模式**并仅指定镜像名称和标签，无需注册表。

<figure><img src="../..//assets/2.15-docker_images_import_simple.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**上传**导入您的镜像。
