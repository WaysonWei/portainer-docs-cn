# Edge堆栈

Edge堆栈功能允许您从单个页面将应用程序部署到多个环境，无论其当前状态如何。

此功能需要您[启用边缘计算](../../../admin/settings/edge.md)功能。

Edge堆栈页面显示部署在您环境和设备上的Edge堆栈列表，包括它们的名称、在相关环境中的部署状态(已确认、镜像预拉取、部署接收和失败，以及通用状态)和创建日期。您可以将鼠标悬停在每个状态条上查看更多详情。

<figure><img src="../..//assets/2.19-edge-stacks-list.png" alt=""><figcaption></figcaption></figure>

您可以点击单个堆栈的名称查看堆栈详情或编辑堆栈：

<figure><img src="../..//assets/2.19-edge-stacks-edit-stack.png" alt=""><figcaption></figcaption></figure>

您还可以在**环境**标签页查看堆栈在环境中的部署详情。

<figure><img src="../..//assets/2.19-edge-stacks-edit-environment.png" alt=""><figcaption></figcaption></figure>

## 添加新堆栈

从菜单中选择**Edge堆栈**然后点击**添加堆栈**。

<figure><img src="../..//assets/2.19-edge-stacks-add.gif" alt=""><figcaption></figcaption></figure>

为堆栈指定一个描述性名称，然后选择一个或多个[Edge组](../groups.md)。

<figure><img src="../..//assets/2.19-edge-stacks-add-name.png" alt=""><figcaption></figcaption></figure>

在**部署类型**中，选择您要执行的部署类型。

此选项可能会根据您选择的[Edge组](../groups.md)自动确定。

<figure><img src="../..//assets/2.15-edge-stacks-add-deptype.png" alt=""><figcaption></figcaption></figure>

在**构建方法**中，从以下选项定义如何部署您的应用：

| 选项       | 概述                                                                        |
| ---------- | ------------------------------------------------------------------------------- |
| 网页编辑器 | 使用Portainer网页编辑器编写或粘贴您的构建文件。              |
| 上传       | 从您的计算机上传构建文件。                                         |
| 仓库       | 使用存储构建文件的GitHub仓库。                               |
| 模板       | 使用Edge堆栈模板。仅适用于**Compose**部署类型。 |

您可以通过按`Ctrl-F`(Mac上为`Cmd-F`)随时在网页编辑器中搜索。

<figure><img src="../..//assets/2.15-edge-stacks-add-buildmethod.png" alt=""><figcaption></figcaption></figure>

### 注册表

如果您的堆栈需要访问私有注册表中的镜像，您可以指定在部署中使用哪个注册表。

<figure><img src="../..//assets/2.15-edge-stacks-add-registry.png" alt=""><figcaption></figcaption></figure>

### 预拉取镜像

默认情况下，Docker将启动堆栈中已有镜像的容器，同时从上游注册表拉取任何其他需要的镜像。在某些情况下，您可能希望在启动堆栈之前等待所有需要的镜像都被拉取到设备上。为此，启用**预拉取镜像**开关。这也有助于避免堆栈中某些镜像无法拉取导致部署不完整或部分部署的问题。

<figure><img src="../..//assets/2.18-edge-stacks-prepull.png" alt=""><figcaption></figcaption></figure>

### 重试部署

如果Edge堆栈部署失败(例如远程Edge环境不可用)，默认情况下Portainer不会尝试重新部署堆栈。如果您希望启用失败部署的重试，可以将**重试部署**开关打开。

<figure><img src="../..//assets/2.18-edge-stacks-retry.png" alt=""><figcaption></figcaption></figure>

当为Edge堆栈启用重试部署且部署失败时，Portainer将：

1. 第一小时内每10秒重试一次部署。
2. 第一小时后，每小时重试一次，持续7天。
3. 7天后，Portainer将停止重试，Edge堆栈将被标记为"失败"状态。

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
