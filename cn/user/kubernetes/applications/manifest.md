# 使用代码添加新应用

有两种方式添加新应用：[手动使用表单](add.md)或自动使用代码。本文介绍如何使用代码添加应用。

使用代码创建不仅限于应用 - 您还可以使用代码部署命名空间、入口、ConfigMaps、secrets、卷等。

首先，从左侧菜单选择**应用**然后点击**从代码创建**。

<figure><img src="../..//assets/2.24.0-kubernetes-applications-manifest-add.gif" alt=""><figcaption></figcaption></figure>

接下来，从**部署来源**部分选择您的部署方法。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-deployfrom.png" alt=""><figcaption></figcaption></figure>

然后，在**部署到**部分选择要部署到的命名空间，并可选地为部署提供堆栈名称。

如果想使用manifest中定义的命名空间，可以将**命名空间**保留为`default`并切换**使用manifest中指定的命名空间**选项。此选项不适用于Helm chart部署。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-namespace.png" alt=""><figcaption></figcaption></figure>

您的下一个选项将取决于选择的部署方法。

## Web编辑器

使用Web编辑器编写或粘贴您的Kubernetes manifest。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-webeditor.png" alt=""><figcaption></figcaption></figure>

可以随时按`Ctrl-F`(Mac上为`Cmd-F`)在Web编辑器中搜索。

准备就绪后，点击**部署**。

## URL

在提供的字段中输入manifest文件的**URL**。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-url.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**部署**。

## 仓库

使用提供的字段输入包含Kubernetes manifests的Git仓库详情。

当从Git部署应用时，Portainer将在部署过程中克隆整个Git仓库。确保有足够的可用空间来容纳此操作。

Portainer的Git部署功能目前不支持使用Git子模块。如果仓库包含子模块，它们将不会作为部署的一部分被拉取。我们[希望在未来的版本中](https://github.com/orgs/portainer/discussions/9767)添加对子模块的支持。

| 字段/选项          | 概述                                                                                                                                                                  |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 认证        | 如果仓库需要认证，请切换此选项。                                                                                                                |
| Git凭据       | 如果启用了**认证**切换并且您已[配置Git凭据](../../account-settings.md#git-credentials)，可以从下拉菜单中选择它们。 |
| 用户名              | 输入Git用户名。                                                                                                                                                  |
| 个人访问令牌 | 输入个人访问令牌或密码。                                                                                                                             |
| 保存凭据       | 选中此选项以保存上面输入的凭据供将来使用，名称由**凭据名称**字段提供。                                          |

<figure><img src="../..//assets/2.16-stacks-add-gitcreds.png" alt=""><figcaption></figcaption></figure>

| 字段/选项          | 概述                                                                                                                                                                                          |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 仓库URL        | 输入仓库URL。如果上面启用了认证，将使用凭据访问仓库。下面的选项将由仓库中找到的内容填充。 |
| 跳过TLS验证 | 切换此选项以跳过验证仓库使用的TLS证书。如果仓库使用自签名证书，这很有用。                                                  |
| 仓库引用  | 选择部署堆栈时使用的引用(例如分支)。                                                                                                                   |
| Manifest路径         | 输入manifest文件相对于仓库根目录的路径。                                                                                                                     |
| 附加路径      | 点击**添加文件**定义作为部署一部分处理的其他manifests或compose文件。                                                                                          |
| GitOps更新        | 切换此选项以启用GitOps更新(见下文)。                                                                                                                                              |

<figure><img src="../..//assets/2.24.0-kubernetes-applications-manifest-git.png" alt=""><figcaption></figcaption></figure>

### GitOps更新

启用GitOps更新使Portainer能够自动更新应用，通过按定义的时间间隔轮询仓库查找更改或使用webhook触发更新。

有关GitOps更新如何工作的更多详情，请查看[此知识库文章](https://portal.portainer.io/knowledge/how-do-automatic-updates-for-stacks-applications-work)。

如果应用配置了GitOps更新并在本地进行更改，这些更改将被Git仓库中的应用定义覆盖。在进行配置更改时请记住这一点。

| 字段/选项   | 概述                                                                                                                                                                                                                                                    |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 机制      | 选择**轮询**或**Webhook**。                                                                                                                                                                                                                     |
| 获取间隔 | 使用**轮询**方法时，选择希望检查Git仓库以获取应用更新的频率。                                                                                                                                   |
| Webhook        | <p>使用<strong>Webhook</strong>方法时，显示要使用的webhook URL。点击<strong>复制链接</strong>将webhook复制到剪贴板。<br>有关webhooks的更多信息，请参阅<a href="webhooks.md">webhook文档</a>。</p> |

<figure><img src="../..//assets/2.19-stacks-add-git-polling.png" alt=""><figcaption><p>使用轮询机制的GitOps更新</p></figcaption></figure>

<figure><img src="../..//assets/2.19-stacks-add-git-webhook.png" alt=""><figcaption><p>使用webhook机制的GitOps更新</p></figcaption></figure>

| 字段/选项          | 概述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 始终应用manifest | <p>启用此设置以强制在指定间隔(或触发webhook时)重新部署应用(kubectl apply)，覆盖本地环境中进行的任何更改，即使Git中的应用没有更新。如果您希望确保Git仓库是应用的单一真实来源，并且对替换本地应用感到满意，这很有用。</p><p></p><p>如果禁用此选项，仅当Portainer检测到远程Git仓库中的更改时才会触发自动更新。</p> |

<figure><img src="../..//assets/2.19-kubernetes-ingress-add-manifest-git-alwaysapply.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**部署**。

## 自定义模板

从**模板**下拉菜单中，选择要使用的自定义模板。根据模板，您可能需要(或能够)设置模板变量以调整部署配置。作为可选步骤，您可以在部署应用之前编辑模板。如果没有自定义模板，将获得指向[自定义模板](../templates/)部分的链接。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-customtemplate.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**部署**。

## Helm chart

选择Helm部署的命名空间后，需要为部署指定**名称**。然后从提供的列表中选择要使用的chart。可以在列表中搜索并按类别筛选。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-helm-select.png" alt=""><figcaption></figcaption></figure>

选择chart后，Portainer将导入chart的`values.yaml`文件，以便您可以配置应用所需的任何参数。可以点击**显示自定义值**选项展开Web编辑器进行任何更改。

<figure><img src="../..//assets/2.20-kubernetes-applications-manifest-helm-webeditor.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**安装**。
