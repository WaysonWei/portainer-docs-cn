# 为容器附加卷

本文介绍如何为正在运行的容器附加新的[卷](../volumes/)。此操作会销毁当前运行的容器并启动一个附加了卷的新容器。

**执行此操作前请务必备份您的数据。**

从菜单中选择**容器**，选择要附加卷的容器，然后点击**复制/编辑**。

<figure><img src="../..//assets/2.15-docker_containers_container_edit.gif" alt=""><figcaption></figcaption></figure>

滚动到**高级容器设置**部分。点击**卷**然后点击**映射附加卷**。

<figure><img src="../..//assets/2.15-docker_containers_container_add_volumes.png" alt=""><figcaption></figcaption></figure>

在**容器**字段中输入路径。在**卷**字段中输入要附加到容器的卷。

<figure><img src="../..//assets/2.15-docker_containers_container_adv_volume_mapping.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**部署容器**。当确认消息出现时，点击**替换**。

<figure><img src="../..//assets/2.15-container-edit-confirm.png" alt=""><figcaption></figcaption></figure>
