# 容器

简单来说，容器是镜像的可运行实例。容器不保存任何持久数据，因此可以根据需要销毁和重新创建。

<figure><img src="../..//assets/2.20-containers-list.png" alt=""><figcaption></figcaption></figure>

当[新镜像指示器](../host/setup.md#other)功能启用时，**镜像最新**列显示容器中的本地镜像是否是最新的，绿色勾表示它们是最新的，橙色叉表示远程仓库中有新版本的镜像可用。灰色连字符表示Portainer无法确定镜像是否有可用更新。

您可以点击搜索框旁边的重新加载按钮重新检查所有容器的镜像更新，或者点击单个容器的镜像指示器图标重新检查该容器的镜像。

有关此工作原理的更多信息，请查看[此知识库文章](https://portal.portainer.io/knowledge/how-does-the-image-update-notification-icon-work)。

要添加新容器，点击**添加容器**。

[add.md](add.md)

容器创建后，您可以检查它、编辑或复制它、切换容器webhook、附加卷、查看日志和统计信息、编辑所有权以及访问其控制台。

[view.md](view.md)

[inspect.md](inspect.md)

[edit.md](edit.md)

[advanced.md](advanced.md)

[webhooks.md](webhooks.md)

[attach-volume.md](attach-volume.md)

[logs.md](logs.md)

[ownership.md](ownership.md)

[stats.md](stats.md)

[console.md](console.md)

如果不再需要容器，可以移除它。

[remove.md](remove.md)
