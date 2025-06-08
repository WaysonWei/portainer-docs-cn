# 添加新堆栈

## 部署新堆栈的选项

Portainer提供四种部署新堆栈的方式：

| 选项                                           | 概述                                                                                                 |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [Web编辑器](add.md#option-1-web-editor)       | 使用我们的Web编辑器以docker-compose格式定义堆栈服务。                                               |
| [上传](add.md#option-2-upload)                 | 如果有`stack.yml`文件，可以从计算机上传并使用它部署堆栈。                                           |
| [Git仓库](add.md#option-3-git-repository)     | 可以使用托管在Git仓库中的docker-compose格式文件。                                                   |
| 自定义模板                                    | 如果创建了[自定义堆栈模板](../templates/custom.md)，可以使用此选项部署。                           |

## 选项1：Web编辑器

从菜单选择**堆栈**，点击**添加堆栈**，给堆栈一个描述性名称，然后选择**Web编辑器**。使用Web编辑器定义服务。

<figure><img src="../..//assets/2.15-docker_add_stack_web_editor.gif" alt=""><figcaption></figcaption></figure>

随时可以按`Ctrl-F`(Mac上是`Cmd-F`)在Web编辑器中搜索。

作为堆栈创建的一部分，可以启用堆栈webhook，允许从仓库远程触发堆栈重新部署等操作。更多信息请参阅[堆栈webhooks](webhooks.md)文档。

<figure><img src="../..//assets/2.15-docker_stack_web_editor_webhook.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，还可以使用Web编辑器定义环境变量。这些变量可用于定义在部署之间会变化的值(例如主机名、数据库名等)。

可以在Portainer中单独设置环境变量，或使用**从.env文件加载变量**上传包含环境变量的文件。定义的环境变量(单独或通过.env文件)可以在compose文件中使用`environment`定义：

```
environment:
  MY_ENVIRONMENT_VARIABLE: ${MY_ENVIRONMENT_VARIABLE}
```

或者，在Docker Standalone和Podman环境中，可以添加`stack.env`作为`env_file`定义，以添加所有单独定义的环境变量以及上传的.env文件中包含的环境变量：

```
env_file:
  - stack.env
```

**注意：** 在Docker Swarm上使用`env_file`定义文件不起作用，因为`docker stack deploy`(在Swarm环境中用于部署堆栈)不支持`env_file`。在Docker Swarm上，需要手动定义每个环境变量。

注意使用环境变量时compose文件不会改变 - 这允许在Portainer中更新变量而无需编辑compose文件本身。在compose文件中仍会看到`${MY_ENVIRONMENT_VARIABLE}`样式的条目。

<figure><img src="../..//assets/2.15-docker_stack_wed_editor_env_var.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**部署堆栈**。

## 选项2：上传

在Portainer中可以从Compose YML文件创建堆栈。为此，从菜单选择**堆栈**，点击**添加堆栈**，然后给堆栈一个描述性名称。

<figure><img src="../..//assets/2.15-docker_add_stack_upload.gif" alt=""><figcaption></figcaption></figure>

选择**上传**，然后从计算机选择Compose文件。

作为堆栈创建的一部分，可以启用堆栈webhook，允许从仓库远程触发堆栈重新部署等操作。更多信息请参阅[堆栈webhooks](webhooks.md)文档。

<figure><img src="../..//assets/2.15-docker_stack_web_editor_webhook.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，输入任何环境变量。这些变量可用于定义在部署之间会变化的值(例如主机名、数据库名等)。

可以在Portainer中单独设置环境变量，或使用**从.env文件加载变量**上传包含环境变量的文件。定义的环境变量(单独或通过.env文件)可以在compose文件中使用`environment`定义：

```
environment:
  MY_ENVIRONMENT_VARIABLE: ${MY_ENVIRONMENT_VARIABLE}
```

或者，可以添加`stack.env`作为`env_file`定义，以添加所有单独定义的环境变量以及上传的.env文件中包含的环境变量：

```
env_file:
  - stack.env
```

注意使用环境变量时compose文件不会改变 - 这允许在Portainer中更新变量而无需编辑compose文件本身，从而保持与本地副本同步。在compose文件中仍会看到`${MY_ENVIRONMENT_VARIABLE}`样式的条目。

<figure><img src="../..//assets/2.15-docker_add_stack_upload_env_var.png" alt=""><figcaption></figcaption></figure>

准备就绪后点击**部署堆栈**。

## 选项3：Git仓库

如果Compose文件托管在Git仓库中，可以从那里部署。从菜单选择**堆栈**，点击**添加堆栈**，然后给堆栈一个描述性名称。

从Git部署堆栈时，Portainer会克隆整个Git仓库作为部署过程的一部分。确保有足够的可用空间来容纳此操作。

Portainer的Git部署功能目前不支持使用Git子模块。如果仓库包含子模块，它们不会作为部署的一部分被拉取。我们[希望在未来的版本中增加支持](https://github.com/orgs/portainer/discussions/9767)。

<figure><img src="../..//assets/2.15-docker_add_stack_git.gif" alt=""><figcaption></figcaption></figure>

选择**Git仓库**，然后输入Git仓库的信息。

任何Git兼容的仓库都应该可以工作。根据需要替换详细信息。

| 字段/选项          | 概述                                                                                                                                                                  |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 认证               | 如果Git仓库需要认证，请切换此选项。                                                                                                                                   |
| Git凭据            | 如果启用了**认证**切换并且[配置了Git凭据](../../account-settings.md#git-credentials)，可以从下拉列表中选择它们。                                                       |
| 用户名             | 输入Git用户名。                                                                                                                                                       |
| 个人访问令牌       | 输入个人访问令牌或密码。                                                                                                                                              |
| 保存凭据           | 选中此选项以保存上面输入的凭据，供将来在**凭据名称**字段提供的名称下使用。                                                                                            |

如果在GitHub中配置了2FA，您的密码就是您的密码。

<figure><img src="../..//assets/2.16-stacks-add-gitcreds.png" alt=""><figcaption></figcaption></figure>

| 字段/选项          | 概述                                                                                                                                                                                          |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 仓库URL            | 输入仓库URL。如果上面启用了认证，将使用凭据访问仓库。下面的选项将由仓库中找到的内容填充。                                                                                                     |
| 跳过TLS验证        | 切换此选项以跳过验证仓库使用的TLS证书。如果仓库使用自签名证书，这很有用。                                                                                                                     |
| 仓库引用           | 选择部署堆栈时要使用的引用(例如分支)。                                                                                                                                                        |
| Compose路径        | 从仓库根目录输入Compose文件的路径。                                                                                                                                                           |
| 附加路径           | 点击**添加文件**添加要由构建解析的其他文件(例如特定环境的compose文件)。                                                                                                                       |
| GitOps更新         | 切换此选项以启用GitOps更新(见下文)。                                                                                                                                                          |

<figure><img src="../..//assets/2.24.0-docker-stacks-add-git.png" alt=""><figcaption></figcaption></figure>

### GitOps更新

Portainer支持自动更新从Git仓库部署的堆栈。要启用此功能，切换**GitOps更新**并配置设置。

有关GitOps更新在后台如何工作的更多详细信息，请查看[此知识库文章](https://portal.portainer.io/knowledge/how-do-automatic-updates-for-stacks-applications-work)。

| 字段/选项       | 概述                                                                                                                                                                                                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 机制            | 选择检查更新时使用的方法：                                                                                                                                                                                                                                                     |
|                 | <p><strong>轮询：</strong>定期从Portainer轮询Git仓库以检查仓库更新。</p><p><strong>Webhook：</strong>生成webhook URL添加到Git仓库以按需触发更新(例如通过GitHub actions)。</p>                                                                                                   |
| 获取间隔        | 如果选择**轮询**，Portainer将检查Git仓库更新的频率。                                                                                                                                                                                                                           |
| Webhook         | 当选择**Webhook**时，显示要在集成中使用的webhook URL。点击**复制链接**将webhook URL复制到剪贴板。                                                                                                                                                                              |

<figure><img src="../..//assets/2.19-stacks-add-git-polling.png" alt=""><figcaption><p>使用轮询时的自动更新</p></figcaption></figure>

<figure><img src="../..//assets/2.19-stacks-add-git-webhook.png" alt=""><figcaption><p>使用webhooks时的自动更新</p></figcaption></figure>

| 字段/选项       | 概述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 重新拉取镜像    | <p>启用此设置以在更新堆栈时始终拉取容器镜像的最新版本。这相当于<code>docker run</code>的<code>--pull=always</code>标志。<br>此选项以前标记为<strong>拉取最新镜像</strong>。</p>                                                                                                                                                                                                                                                                                                                                                                          |
| 强制重新部署    | <p>启用此设置以强制在指定间隔(或触发webhook时)重新部署堆栈，覆盖本地环境中已进行的任何更改，即使Git中的堆栈没有更新。如果想确保Git仓库是堆栈的真实来源，并且乐意替换本地堆栈，这很有用。</p><p>如果禁用此选项，自动更新仅在Portainer检测到远程Git仓库中的更改时触发。</p>                                                                                                                                                                                                                                                                                 |

<figure><img src="../..//assets/2.19-stacks-add-git-repull-force.png" alt=""><figcaption></figcaption></figure>

### 相对路径卷

当切换**启用相对路径卷**为开启时，可以在compose文件中指定相对路径引用。Portainer将创建所需的目录结构并用Git仓库中的相关文件填充目录。

此功能仅在Portainer商业版中可用。

在Docker Standalone和Podman环境中，在**本地文件系统路径**字段中指定要在主机文件系统上创建文件的路径。

确保此目录存在于本地文件系统上并且可写。

<figure><img src="../..//assets/2.17-stacks-add-relativepath.png" alt=""><figcaption></figcaption></figure>

在Docker Swarm环境中，在**网络文件系统路径**字段中指定要创建文件的路径。

确保此路径在所有Docker Swarm节点上都可用并且可写。

<figure><img src="../..//assets/2.17-stacks-add-relativepath-swarm.png" alt=""><figcaption></figcaption></figure>

有关此功能如何工作的更多详细信息，请查看[此文章](../../../advanced/relative-paths.md)。

### 环境变量

作为可选步骤，还可以设置环境变量。这些变量可用于定义在部署之间会变化的值(例如主机名、数据库名等)。

可以在Portainer中单独设置环境变量，或使用**从.env文件加载变量**上传包含环境变量的文件。定义的环境变量(单独或通过.env文件)可以在compose文件中使用`environment`定义：

```
environment:
  MY_ENVIRONMENT_VARIABLE: ${MY_ENVIRONMENT_VARIABLE}
```

或者，可以添加`stack.env`作为`env_file`定义，以添加所有单独定义的环境变量以及上传的.env文件中包含的环境变量：

```
env_file:
  - stack.env
```

注意使用环境变量时compose文件不会改变 - 这允许在Portainer中更新变量而无需编辑compose文件本身，从而保持与Git仓库同步。在compose文件中仍会看到`${MY_ENVIRONMENT_VARIABLE}`样式的条目。

<figure><img src="../..//assets/2.15-docker_stack_wed_editor_env_var.png" alt=""><figcaption></figcaption></figure>

如果需要输入环境变量，然后点击**部署堆栈**。
