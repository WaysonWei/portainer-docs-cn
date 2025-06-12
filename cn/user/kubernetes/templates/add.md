# 添加新的自定义模板

## 创建模板

从菜单中选择 **Custom Templates** 然后点击 **Add Custom Template**。

<figure><img src="../..//assets/2.19-kubernetes-templates-add.gif" alt=""><figcaption></figcaption></figure>

填写表单，参考下表：

| Field/Option | Overview                                                                                         |
| ------------ | ------------------------------------------------------------------------------------------------ |
| Title        | 输入自定义模板的标题。这将作为模板部署时的显示名称。 |
| Description  | 输入模板的描述。                                                             |
| Note         | 可选步骤，记录模板的额外信息。                           |
| Icon URL     | 可选，输入用作模板图标的图片URL。                        |

<figure><img src="../..//assets/2.15-kubernetes_create_custom_template.png" alt=""><figcaption></figcaption></figure>

接下来，选择 **Build method**。

## 选择构建方法

### 方法 1: Web 编辑器

在 web 编辑器中定义或粘贴您的清单文件内容。当使用自定义模板部署应用程序时，您将有机会在部署前编辑清单。

您可以通过按 `Ctrl-F`（Mac 上是 `Cmd-F`）随时在 web 编辑器中搜索。




<figure><img src="../..//assets/2.19-kubernetes-templates-add-web.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击 **Create custom template**。

### 方法 2: 上传

如果您本地有清单文件，可以直接上传到 Portainer。点击 **Select file** 浏览选择文件。



<figure><img src="../..//assets/2.19-kubernetes-templates-add-upload.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击 **Create custom template**。

### 方法 3: 仓库

如果您的模板在 Git 仓库中，可以将其添加到自定义模板。输入访问 Git 仓库所需的详细信息。

| Field/Option          | Overview                                                                                                                                  |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Authentication        | 如果您的仓库需要认证，请开启此选项。                                                                         |
| Git credentials       | 如果已配置凭据，可以从下拉菜单中选择要使用的凭据集。                                                      |
| Username              | 输入您的 Git 用户名。                                                                                                                  |
| Personal access token | 输入您的个人访问令牌或密码。                                                                                             |
| Repository URL        | 输入您的 Git 仓库 URL。                                                                                                     |
| Repository reference  | 选择要使用的仓库引用。这将自动填充您仓库中可用的引用。             |
| Manifest path         | 输入仓库中清单文件的路径和文件名。                                                                       |
| Skip TLS Verification | 开启此选项可跳过仓库的 TLS 验证。这在您使用自签名证书时很有用。 |

<figure><img src="../..//assets/2.19-kubernetes-templates-add-git.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击 **Create custom template**。

## 模板中的变量

自定义模板支持使用变量来进一步定制部署的堆栈。堆栈可以定义一个变量，用户可以在部署时调整该变量。

此功能仅在 Portainer Business Edition 中可用。

变量在堆栈中用 `{{ }}` 标识。例如，以下堆栈提供了一个 `REPLICA_COUNT` 变量：

<figure><img src="../..//assets/2.19-kubernetes-templates-add-variables.png" alt=""><figcaption></figcaption></figure>

当定义变量时，会出现选项来自定义变量在部署堆栈时的显示方式。您可以设置 **label**、**description** 和 **default value**。

当模板部署时，任何已配置的变量都是可编辑的：

<figure><img src="../..//assets/2.19-kubernetes-templates-add-variables-deploy.png" alt=""><figcaption></figcaption></figure>
