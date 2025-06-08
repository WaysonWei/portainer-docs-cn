# 构建新镜像

有三种方式可以构建新镜像。

在多节点环境中，构建的镜像仅会出现在您在**部署**部分选择的节点上。要使镜像对所有节点可用，请考虑[添加注册表](../../../admin/registries/add/)到Portainer。

使用Portainer构建镜像时，无法使用引用主机上文件的`ADD`或`COPY`命令。我们建议使用`wget`或类似工具从HTTP/S URL获取文件。

## 方法1：使用Portainer网页编辑器

从菜单中选择**镜像**，然后点击**构建新镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_image.gif" alt=""><figcaption></figcaption></figure>

为镜像输入描述性名称(可以输入多个名称)，在**构建方法**下选择**网页编辑器**选项，然后在网页编辑器中编写您的Dockerfile。

您可以随时按`Ctrl-F`(Mac上为`Cmd-F`)在网页编辑器中搜索。

<figure><img src="../..//assets/2.15-docker_images_build_web_editor.png" alt=""><figcaption></figcaption></figure>

可选地，您可以点击**选择文件**上传一个或多个本地文件包含到镜像中，然后在Dockerfile中引用它们。

<figure><img src="../..//assets/2.16-images-build-upload.png" alt=""><figcaption></figcaption></figure>

选择要保存镜像的节点(如果在多节点环境中)，然后点击**构建镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_deployment.png" alt=""><figcaption></figcaption></figure>

构建完成后，选择**输出**选项卡查看构建历史和结果。

## 方法2：上传Dockerfile

如果有现有的Dockerfile，可以上传到Portainer并用它构建镜像。

从菜单中选择**镜像**，然后点击**构建新镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_image_upload.gif" alt=""><figcaption></figcaption></figure>

为镜像输入描述性名称(可以输入多个名称)，在**构建方法**下选择**上传**选项，然后浏览并上传Dockerfile。

<figure><img src="../..//assets/2.15-docker_images_build_upload.png" alt=""><figcaption></figcaption></figure>

向下滚动并选择要保存镜像的节点(如果在多节点环境中)，然后点击**构建镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_deployment.png" alt=""><figcaption></figcaption></figure>

构建完成后，选择**输出**选项卡查看构建历史和结果。

## 方法3：从URL提供Dockerfile

如果Dockerfile托管在互联网上(在tarball或公共GitHub仓库中)，可以通过URL直接下载到Portainer。

从菜单中选择**镜像**，然后点击**构建新镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_image_URL.gif" alt=""><figcaption></figcaption></figure>

为镜像输入描述性名称(可以输入多个名称)，在**构建方法**下选择**上传**选项，然后输入文件的**URL**以及tarball或仓库中的**Dockerfile路径**。

<figure><img src="../..//assets/2.15-docker_images_build_URL.png" alt=""><figcaption></figcaption></figure>

向下滚动并选择要保存镜像的节点(如果在多节点环境中)，点击**构建镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_deployment.png" alt=""><figcaption></figcaption></figure>

构建完成后，选择**输出**选项卡查看构建历史和结果。
