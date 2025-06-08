# 导出镜像

您可以导出存储在任何节点上的任何Docker镜像。这在需要将容器从一台主机迁移到另一台主机，或简单地对镜像进行备份时非常有用。

如果导出容器到tar文件，卷不会随其一起导出。您需要使用其他方法保存这些卷中的数据。

从菜单中选择**镜像**，选择要导出的镜像然后点击**导出此镜像**。

<figure><img src="../..//assets/2.15-docker_images_build_image_export.gif" alt=""><figcaption></figcaption></figure>

当警告消息出现时，点击**继续**。

<figure><img src="../..//assets/2.15-images-export-confirm.png" alt=""><figcaption></figcaption></figure>

镜像下载完成后，将出现成功消息，您的浏览器应自动下载生成的tar文件。
