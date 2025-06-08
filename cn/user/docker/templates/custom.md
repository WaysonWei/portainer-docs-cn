# 自定义模板

自定义模板可用于简化容器或堆栈的部署流程。

您也可以[从现有部署的堆栈创建模板](../stacks/template.md)。

## 查看自定义模板列表

要查看自定义模板列表，从菜单展开**模板**然后选择**自定义**。

<figure><img src="../..//assets/2.20-templates-custom.gif" alt=""><figcaption></figcaption></figure>

## 创建新的自定义模板

### 输入基本信息

点击**添加自定义模板**然后填写详细信息，参考下方表格作为指南：

| 字段/选项       | 说明                                                                                    |
| --------------- | --------------------------------------------------------------------------------------- |
| 标题            | 为模板指定一个描述性名称。                                                              |
| 描述            | 输入模板包含内容的简要说明。                                                            |
| 备注            | 记录模板的任何额外信息(可选)。                                                          |
| 图标            | 输入模板在列表中显示时使用的图标URL(可选)。                                             |
| 平台            | 选择模板兼容的平台。选项为**Linux**或**Windows**。                                      |
| 类型            | 选择模板类型。选项为**独立/Podman**或**Swarm**。                                        |

<figure><img src="../..//assets/2.22.0-templates-custom-new.png" alt=""><figcaption></figcaption></figure>

### 选择构建方法

接下来，选择适合您需求的构建方法。您可以使用网页编辑器手动输入docker-compose文件，从本地计算机上传`docker-compose.yml`文件，或从Git仓库拉取compose文件。

#### 网页编辑器

将docker-compose文件内容粘贴到提供的框中。完成所有详细信息后，点击**创建自定义模板**。

您可以随时按`Ctrl-F`(Mac上为`Cmd-F`)在网页编辑器中搜索。

<figure><img src="../..//assets/2.20-templates-custom-add-webeditor.png" alt=""><figcaption></figcaption></figure>

#### 上传

点击**选择文件**浏览要上传的docker-compose文件。完成所有详细信息后，点击**创建自定义模板**。

<figure><img src="../..//assets/2.20-templates-custom-add-upload.png" alt=""><figcaption></figcaption></figure>

#### Git仓库

填写Git仓库的详细信息。

| 字段/选项          | 说明                                                                                     |
| ------------------ | ---------------------------------------------------------------------------------------- |
| 认证              | 如果您的Git仓库需要认证，请启用此选项。                                                  |
| Git凭据           | 启用认证后，选择预设的Git凭据集或留空以提供新凭据。                                      |
| 用户名            | 启用认证后，输入您的Git用户名。                                                          |
| 个人访问令牌      | 启用认证后，输入您的个人访问令牌或密码。                                                 |
| 保存凭据          | 启用认证并提供新凭据后，可以勾选此框并输入名称以保存这些凭据供将来使用。                 |
| 仓库URL           | 输入您的Git仓库URL。                                                                     |
| 仓库引用          | 选择仓库引用以定义要拉取的分支或标签。                                                   |
| Compose路径        | 输入仓库内docker-compose文件的路径。                                                     |
| 跳过TLS验证       | 启用此选项可跳过Git仓库TLS证书的验证。                                                   |

<figure><img src="../..//assets/2.20-templates-custom-add-git.png" alt=""><figcaption></figcaption></figure>

输入所有详细信息后，点击**创建自定义模板**。

## 模板中的变量

自定义模板支持使用变量来进一步自定义部署的堆栈。堆栈可以定义一个变量，用户可以在部署时调整该变量。

此功能仅在Portainer商业版中可用。

变量在堆栈中用`{{ }}`标识。例如，以下堆栈提供了一个`MYSQL_PASSWORD`变量：

<figure><img src="../..//assets/2.15-docker-templates-custom-variables-set.png" alt=""><figcaption></figcaption></figure>

定义变量后，会出现选项来自定义变量在部署堆栈时的显示方式。您可以设置**标签**、**描述**和**默认值**。

部署模板时，任何已配置的变量都是可编辑的：

<figure><img src="../..//assets/2.15-docker-templates-custom-variables-create.png" alt=""><figcaption></figcaption></figure>
