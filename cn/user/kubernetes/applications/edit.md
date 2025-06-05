# 编辑应用

从菜单选择**应用**，选择要编辑的应用，然后点击**编辑此应用**。

<figure><img src="../..//assets/2.20-kubernetes-applications-edit.gif" alt=""><figcaption></figcaption></figure>

您的编辑选项取决于应用最初是如何部署的。

无论部署方式如何，在Portainer商业版中都可以通过YAML标签页[直接编辑应用的YAML](inspect.md#yaml-tab)。

## 从Git仓库部署的应用

如果应用是[从Git仓库部署的](manifest.md#repository)，您可以在需要时从仓库重新部署。您将看到应用部署的仓库URL、当前部署的版本以及用于部署的文件。

<figure><img src="../..//assets/2.19-kubernetes-applications-edit-git-info.png" alt=""><figcaption></figcaption></figure>

如果需要，您可以在此重新配置GitOps更新、仓库引用和认证。如果启用了变更窗口，相关信息也会显示在此处。

<figure><img src="../..//assets/2.20-kubernetes-applications-edit-gitops.png" alt=""><figcaption></figcaption></figure>

如果要重新部署，点击**拉取并更新应用**。如果只是更新仓库设置而不需要重新部署，点击**保存设置**。

## 从Web编辑器部署的应用

如果应用是从Web编辑器部署的，您将能够手动编辑manifest。

您可以随时按`Ctrl-F`(Mac上为`Cmd-F`)在Web编辑器中搜索。

<figure><img src="../..//assets/2.20-kubernetes-applications-edit-webeditor.png" alt=""><figcaption></figcaption></figure>

进行所需更改后点击**更新应用**。

## 从表单或Helm部署的应用

当编辑从表单或Helm部署的应用时，您将能够使用相同的表单更新配置。详情请参阅[使用表单添加新应用](add.md)。
