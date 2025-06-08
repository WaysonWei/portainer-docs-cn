# 添加新的Edge堆栈

从菜单中选择**Edge堆栈**然后点击**添加堆栈**。

<figure><img src="../..//assets/2.20-edge-stacks-add.gif" alt=""><figcaption></figcaption></figure>

为堆栈指定一个描述性名称，然后选择一个或多个[Edge组](../groups.md)。

<figure><img src="../..//assets/2.19-edge-stacks-add-name.png" alt=""><figcaption></figcaption></figure>

在**部署类型**中，选择您要执行的部署类型。

此选项可能会根据您选择的[Edge组](../groups.md)中的环境自动确定。

<figure><img src="../..//assets/2.20-edge-stacks-add-deploymenttype.png" alt=""><figcaption></figcaption></figure>

在**构建方法**中，从以下选项定义如何部署您的应用：

| 选项       | 概述                                                                        |
| ---------- | ------------------------------------------------------------------------------- |
| 网页编辑器 | 使用Portainer网页编辑器编写或粘贴您的构建文件。              |
| 上传       | 从您的计算机上传构建文件。                                         |
| 仓库       | 使用存储构建文件的GitHub仓库。                               |
| 模板       | 使用Edge堆栈模板。仅适用于**Compose**部署类型。 |

<figure><img src="../..//assets/2.20-edge-stacks-add-buildmethod.png" alt=""><figcaption></figcaption></figure>

## 网页编辑器

使用网页编辑器定义您的部署服务。

您可以通过按`Ctrl-F`(Mac上为`Cmd-F`)随时在网页编辑器中搜索。

<figure><img src="../..//assets/2.19-edge-stacks-edit-webeditor.png" alt=""><figcaption></figcaption></figure>

## 上传

点击**选择文件**从您的计算机上传包含堆栈定义的文件。

<figure><img src="../..//assets/2.19-edge-stacks-add-upload.png" alt=""><figcaption></figcaption></figure>

## 仓库

输入有关您的Git仓库的信息，以便从Git部署Edge堆栈。

Portainer的Git部署功能目前不支持Git子模块。如果您的仓库包含子模块，它们将不会作为部署的一部分被拉取。我们[希望在未来的版本中](https://github.com/orgs/portainer/discussions/9767)添加对子模块的支持。

| 字段/选项          | 概述                                                                                                                         |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 认证        | 如果您的Git仓库需要认证，请启用此选项。                                                                   |
| Git凭据       | 如果启用了**认证**选项并且您已配置了Git凭据，可以从此下拉菜单中选择它们。     |
| 用户名              | 输入您的Git用户名。                                                                                                         |
| 个人访问令牌 | 输入您的个人访问令牌或密码。                                                                                    |
| 保存凭据       | 勾选此选项以保存上面输入的凭据供将来使用，名称在**凭据名称**字段中提供。 |

如果您在GitHub中配置了2FA，您的密码就是您的密码。

<figure><img src="../..//assets/2.19-edge-stacks-add-git-auth.png" alt=""><figcaption></figcaption></figure>

| 字段/选项                 | 概述                                                                                                                                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 仓库URL               | 输入仓库URL。如果上面启用了认证，将使用凭据访问仓库。下面的选项将由仓库中找到的内容填充。 |
| 仓库引用         | 选择部署堆栈时使用的引用(例如分支)。                                                                                                                   |
| Compose路径 / manifest路径 | 输入从仓库根目录到Compose或manifest文件的路径。                                                                                                                   |
| 附加路径             | 点击**添加文件**添加要由构建解析的其他文件(例如环境特定的compose或manifest文件)。                                                             |
| GitOps更新               | 启用此选项以启用GitOps更新(见下文)。                                                                                                                                              |
| 跳过TLS验证        | 启用此选项以跳过对仓库使用的TLS证书的验证。如果您的仓库使用自签名证书，这很有用。                                                  |

<figure><img src="../..//assets/2.19-stacks-add-git.png" alt=""><figcaption></figcaption></figure>

### GitOps更新

Portainer支持自动更新从Git仓库部署的Edge堆栈。要启用此功能，请打开**GitOps更新**并配置您的设置。

有关自动更新在后台如何工作的更多详细信息，请查看[此知识库文章](https://portal.portainer.io/knowledge/how-do-automatic-updates-for-stacks-applications-work)。

| 字段/选项   | 概述                                                                                                                                                                                                                                                                            |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 机制      | 选择检查更新时使用的方法:                                                                                                                                                                                                                                 |
|                | <p><strong>轮询:</strong> 定期从Portainer轮询Git仓库以检查仓库更新。</p><p><strong>Webhook:</strong> 生成一个webhook URL添加到您的Git仓库以按需触发更新(例如通过GitHub actions)。</p> |
| 获取间隔 | 如果选择**轮询**，Portainer将检查Git仓库更新的频率。                                                                                                                                                                                          |
| Webhook        | 当选择**Webhook**时，显示要在集成中使用的webhook URL。点击**复制链接**将webhook URL复制到剪贴板。                                                                                                                                    |

<figure><img src="../..//assets/2.19-stacks-add-git-polling.png" alt=""><figcaption><p>使用轮询时的GitOps更新</p></figcaption></figure>

<figure><img src="../..//assets/2.19-stacks-add-git-webhook.png" alt=""><figcaption><p>使用webhooks时的GitOps更新</p></figcaption></figure>

|                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 重新拉取镜像      | 当选择**Webhook**时，显示要在集成中使用的webhook URL。点击**复制链接**将webhook URL复制到剪贴板。                                                                                                                                                                                                                                                                                                                                                                                                            |
| 强制重新部署 | <p>启用此设置以强制在指定间隔(或触发webhook时)重新部署堆栈，覆盖本地环境中已做的任何更改，即使Git中的堆栈没有更新。如果您希望确保Git仓库是堆栈的真实来源并且对替换本地堆栈感到满意，这很有用。</p><p>如果禁用此选项，仅当Portainer检测到远程Git仓库中的更改时才会触发自动更新。</p> |

<figure><img src="../..//assets/2.19-stacks-add-git-repull-force.png" alt=""><figcaption></figcaption></figure>

### 相对路径卷

当您将**启用相对路径卷**切换为开时，您可以在compose文件中指定相对路径引用。Portainer将创建所需的目录结构并用Git仓库中的相关文件填充目录。此功能仅适用于Docker独立和Docker Swarm环境。

如果您之前启用了[GitOps Edge配置](add.md#gitops-edge-configurations)，那里设置的文件系统路径也将用于相对路径卷功能。

在Docker独立环境中，在**本地文件系统路径**字段中指定您希望在主机文件系统上创建文件的路径。

确保此目录存在于本地文件系统上并且可写。

<figure><img src="../..//assets/2.17-stacks-add-relativepath.png" alt=""><figcaption></figcaption></figure>

在Docker Swarm环境中，在**网络文件系统路径**字段中指定您希望创建文件的路径。

确保此路径在您的所有Docker Swarm节点上都可用并且可写。

<figure><img src="../..//assets/2.17-stacks-add-relativepath-swarm.png" alt=""><figcaption></figcaption></figure>

有关此功能如何工作的更多详细信息，请查看[此文章](../../../advanced/relative-paths.md)。

### GitOps Edge配置

您还可以选择从Git仓库部署设备特定的配置到将部署Edge堆栈的设备。要使用此功能，启用**GitOps Edge配置**开关，输入**本地**或**远程文件系统路径**，**目录**(相对于Git仓库的根目录)并选择与您的配置对应的**设备**或**组匹配规则**。

如果您之前启用了[相对路径卷](add.md#relative-path-volumes)，那里设置的文件系统路径也将用于GitOps Edge配置功能。

<figure><img src="../..//assets/2.20-edge-stacks-add-git-edgeconfigs.png" alt=""><figcaption></figcaption></figure>

如果您同时设置了**设备匹配规则**和**组匹配规则**，设备匹配规则将优先。如果无法匹配设备匹配规则(换句话说，如果无法找到与设备名称匹配的文件或文件夹名)，Portainer将回退到组匹配规则。

在您定义的**目录**下的Git仓库中，您应该具有与将部署堆栈的设备的Portainer Edge ID或Edge组对应的文件名或文件夹名(取决于您的**匹配规则**选择)。您可以在堆栈文件中使用`PORTAINER_EDGE_ID`和`PORTAINER_EDGE_GROUP`环境变量引用此ID。

您可以在**环境**下找到Edge环境的Edge ID，选择环境，并注意**Edge信息**框中的**Edge标识符**值。它将如下所示：

`73149964-56f4-473b-81b3-5ecdc397e490`

例如，当使用文件夹名匹配和`config`目录时，您可以使用以下语法：

```
version: '3'

services:
  myservice:
    image: myimage:latest
    volumes:
      - ./config/${PORTAINER_EDGE_ID}:/my-device-config
```

在此示例中，部署堆栈的每个Edge设备将从Git仓库的`config`目录中挂载其特定设备(基于Portainer Edge ID)文件夹到容器中的`/my-device-config`文件夹。

如果您将堆栈部署到GitOps Edge配置目录中没有与Portainer Edge ID对应的文件或文件夹的设备，堆栈将正常部署但没有部署设备特定的配置。

## 模板

从**模板**下拉菜单中选择一个Edge堆栈模板进行部署，并根据需要进行任何配置调整。

<figure><img src="../..//assets/2.19-edge-stacks-add-template.png" alt=""><figcaption></figcaption></figure>

## 附加设置

### Webhooks

对于网页编辑器、上传和模板构建方法，您可以选择启用Edge堆栈webhook。此webhook将允许您通过向特定URL发送POST请求来触发堆栈更新，指示Portainer拉取关联镜像的最新版本并重新部署堆栈。

对于Git部署的堆栈，此功能可通过[GitOps更新](add.md#gitops-updates)获得。

<figure><img src="../..//assets/2.19-edge-stacks-add-webhook.png" alt=""><figcaption></figcaption></figure>

### 环境变量

作为可选步骤，您还可以设置环境变量。您可以使用这些变量来定义在部署之间会变化的compose文件中的值(例如主机名、数据库名称等)。

此功能仅适用于Docker独立和Docker Swarm环境。

环境变量可以在Portainer中单独设置，也可以使用**从.env文件加载变量**上传包含环境变量的文件。您定义的环境变量(单独或通过.env文件)将可用于在compose文件中使用`environment`定义：

```
environment:
  MY_ENVIRONMENT_VARIABLE: ${MY_ENVIRONMENT_VARIABLE}
```

或者，您可以添加`stack.env`作为`env_file`定义，以添加您单独定义的所有环境变量以及上传的.env文件中包含的环境变量：

```
env_file:
  - stack.env
```

请注意，使用环境变量时不会更改compose文件 - 这允许在Portainer中更新变量而无需编辑compose文件本身，这将使其与Git仓库不同步。您仍将在compose文件中看到`${MY_ENVIRONMENT_VARIABLE}`样式的条目。

<figure><img src="../..//assets/2.15-docker_stack_wed_editor_env_var.png" alt=""><figcaption></figcaption></figure>

### 注册表

如果您的堆栈需要访问私有注册表中的镜像，您可以指定在部署中使用哪个注册表。

<figure><img src="../..//assets/2.15-edge-stacks-add-registry.png" alt=""><figcaption></figcaption></figure>

### 预拉取镜像

默认情况下，Docker将启动堆栈中已有镜像的容器，同时从上游注册表拉取任何其他需要的镜像。在某些情况下，您可能希望在启动堆栈之前等待所有需要的镜像都被拉取到设备上。为此，启用**预拉取镜像**开关。这也有助于避免堆栈中某些镜像无法拉取导致部署不完整或部分部署的问题。

<figure><img src="../..//assets/2.18-edge-stacks-prepull.png" alt=""><figcaption></figcaption></figure>

### 重试部署

如果Edge堆栈部署失败(例如远程Edge环境不可用)，默认情况下Portainer不会尝试重新部署堆栈。如果您希望启用失败部署的重试，可以将**重试部署**开关打开，并将**重试时间**设置为希望Portainer尝试部署堆栈的时间长度。

<figure><img src="../..//assets/2.25.0-edge-stacks-retry-deployment.png" alt=""><figcaption></figcaption></figure>

当达到**重试时间**中选择的时间时，Portainer将停止重试，Edge堆栈将被标记为"失败"状态。

### 更新配置

此部分允许您定义堆栈更新在Edge设备上的部署方式。您可以选择**一次性部署到所有Edge设备**，或选择**并行Edge设备**指定同时更新的设备数量。

这些设置**不**适用于Edge堆栈的_初始_部署。这些仅适用于堆栈部署_后_更新时的过程。

<figure><img src="../..//assets/2.19-edge-stacks-updateconfigs.png" alt=""><figcaption></figcaption></figure>

如果选择**并行Edge设备**，您可以选择静态组大小或指数级推出策略。对于静态组大小，选择**设备数量**选项并指定您的组大小。

<figure><img src="../..//assets/2.19-edge-stacks-parallel-staticgroups.png" alt=""><figcaption></figcaption></figure>

对于指数级推出，选择**指数级推出**选项并指定起始设备数量，然后选择应用于初始大小的乘数。例如，选择起始大小为5和乘数为2，堆栈更新将先部署到5台设备，然后是10台(5 x 2)，然后是20台(10 x 2)，依此类推。

<figure><img src="../..//assets/2.19-edge-stacks-parallel-exponential.png" alt=""><figcaption></figcaption></figure>

使用并行推出时，您还可以指定**超时**(分钟)，在此之后Portainer认为更新失败，以及**更新延迟**(分钟)，即每组更新之间的间隔时间。

此外，您可以定义更新失败时将采取的**更新失败操作**：
* **继续**将转到下一组设备进行更新。
* **暂停**将停止更新过程，但已部署更新的设备将保持更新状态。
* **回滚**将停止更新过程并回滚已更新设备上的更新。

<figure><img src="../..//assets/2.19-edge-stacks-parallel-failureaction.png" alt=""><figcaption></figcaption></figure>

配置完成后，点击**部署堆栈**。
