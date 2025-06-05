# 常规设置

## 应用设置

### 快照间隔

定义环境数据快照的拍摄频率。数据快照包含在环境主页上显示的信息以及其他基本信息。默认为每5分钟一次。

### Edge Agent默认轮询频率

此设置定义Edge Agent与Portainer实例检查时使用的默认间隔。

### 使用自定义Logo

用您自己的Logo替换我们的Logo。切换开启并输入Logo的URL。推荐尺寸为155px × 55px。

### 允许收集匿名统计信息

我们收集有关Portainer安装的匿名信息以帮助产品开发。您可以在安装期间选择退出，或随时关闭此设置。

<figure><img src="..//assets/2.20-settings-general-application.png" alt=""><figcaption></figcaption></figure>

### 登录屏幕横幅

此设置允许您指定一个自定义文本横幅，该横幅将出现在所有用户的登录屏幕上。可用于提供信息详情、警告消息或任何您需要的内容。要启用此功能，请切换**登录屏幕横幅**选项开启，并在**详情**框中输入您的消息。

<figure><img src="..//assets/2.16-settings-login-screen-banner.png" alt=""><figcaption></figcaption></figure>

您的消息将显示在登录屏幕上。

<figure><img src="..//assets/2.16-settings-login-screen-banner-example.png" alt=""><figcaption></figcaption></figure>

### 应用模板

您可以使用Portainer内置的应用模板集部署容器和服务，或者[替换为您自己的](../../advanced/app-templates/build.md)模板集。一旦您有了包含模板定义的JSON文件，您可以在此处提供其URL。

<figure><img src="..//assets/2.15-settings-settings-2.png" alt=""><figcaption></figcaption></figure>

## Kubernetes设置

### Helm仓库

如果您希望使用自己的Helm仓库替代我们默认包含的Bitnami仓库，可以在此处输入URL。

<figure><img src="..//assets/2.15-settings-settings-3.png" alt=""><figcaption></figcaption></figure>

### Kubeconfig

在此处您可以从下拉菜单中选择[导出的kubeconfig文件](../../user/kubernetes/kubeconfig.md)的过期时间。新的过期时间仅适用于此值更改后创建的配置。管理员还可以在此处为非管理员用户禁用Kubeconfig下载。

<figure><img src="..//assets/2.22.0-settings-kubernetes-kubeconfig.png" alt=""><figcaption></figcaption></figure>

当Portainer重启时，`kubeconfig`文件中使用的令牌将失效——无论**Kubeconfig过期**设置为何值。在这种情况下，您需要重新下载`kubeconfig`文件。


### KubeShell

此选项允许管理员为非管理员用户禁用KubeShell访问。

<figure><img src="..//assets/2.22.0-settings-kubernetes-kubeshell.png" alt=""><figcaption></figcaption></figure>

### 部署选项

在本节中，您可以配置各种Kubernetes特定的部署选项。

| 字段/选项                                            | 概述                                                                                                                                                                                                           |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 强制基于代码的部署                           | 启用此选项可在部署应用程序时隐藏"使用表单添加"按钮，并防止通过表单添加或编辑Kubernetes资源。                                                               |
| 允许使用Web编辑器和自定义模板                | 当强制基于代码部署时，启用此选项以允许在部署应用程序时使用Web编辑器和自定义模板。                                                                         |
| 允许通过URL指定清单                | 当强制基于代码部署时，启用此选项以允许在部署应用程序时使用URL选项。                                                                                                 |
| 允许按环境覆盖                          | 启用此选项以允许按环境覆盖上述强制选项。                                                                                                                    |
| 要求在应用程序上添加注释                          | 启用此选项以要求部署必须完成"注释"字段才能部署。此设置目前仅适用于通过表单部署时。                                                          |
| 允许Kubernetes环境使用堆栈功能 | 启用此选项以允许将Kubernetes部署分组为"堆栈"，帮助组织和管理相关工作负载。禁用此选项将隐藏Kubernetes环境中的堆栈功能。 |

<figure><img src="..//assets/2.20-settings-general-kubernetes-deployment.png" alt=""><figcaption></figcaption></figure>

## Kubernetes Helm仓库的证书授权文件

本节允许您提供证书授权(CA)文件，用于从Portainer到Helm仓库的HTTPS连接。如果您的Helm仓库使用的TLS证书由自定义CA签名，这将非常有用，并且适用于上面配置的Helm仓库以及按环境配置的Helm仓库。

此功能仅在[Portainer商业版](https://www.portainer.io/business-upsell?from=ca-file)中可用。

<figure><img src="..//assets/2.18-settings-helmcafile.png" alt=""><figcaption></figcaption></figure>

## SSL证书

安装期间，Portainer默认创建一个自签名的SSL证书，用于加密Portainer Server与最终用户之间以及Portainer Server与Portainer Agent之间的通信。您可以用自己的证书替换此证书。


我们建议在证书中包含完整的证书链以确保兼容性。如果您没有证书的完整链，请咨询您的证书提供商或使用[What's My Chain Cert?](https://whatsmychaincert.com/)生成它。


<figure><img src="..//assets/2.15-settings-settings-ssl-1.png" alt=""><figcaption></figcaption></figure>

### 强制HTTPS

如果您的Portainer Server实例配置为监听`9443`(HTTPS)和`9000`(HTTP)端口，您可以切换**强制HTTPS**开启以禁用`9000`端口的监听。


在启用此选项**之前**，请确保您的HTTPS配置正常工作。否则可能导致您[被锁定在Portainer安装之外](https://portal.portainer.io/knowledge/i-enabled-force-https-only-and-now-im-locked-out-of-portainer-how-do-i-get-back-in)。



在启用此功能前，请确保所有Edge agent已正确配置为使用HTTPS通信。


<figure><img src="..//assets/2.15-settings-settings-ssl-force.png" alt=""><figcaption></figcaption></figure>

完成更改后，点击**应用更改**。

## 实验性功能

本节允许您启用Portainer的实验性功能用于您的部署。这些功能处于早期开发阶段，仅经过有限测试，提供给用户以便在开发早期阶段收集反馈。


在生产部署中启用实验性功能应谨慎操作，风险自负。


| Field/Option              | Overview                                                                                                                                                                                     |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Enable OpenAI integration | 切换此选项以启用OpenAI集成。启用后，各个用户需要在其账户设置中添加他们的OpenAI密钥才能使用此功能。 |

<figure><img src="..//assets/2.18.3-settings-experimental.png" alt=""><figcaption></figcaption></figure>

## 隐藏容器

通过容器标签阻止容器出现在Portainer UI中。输入标签的名称和值，然后点击**添加过滤器**。具有匹配标签的容器将被隐藏。

<figure><img src="..//assets/2.15-settings-settings-hiddencontainers.png" alt=""><figcaption></figcaption></figure>

## 备份Portainer

此设置包含Portainer存储在`/data`卷中的所有信息，归档为`tar.gz`文件，并可选择使用密码加密。此归档文件是恢复Portainer所需的全部内容。


此备份**仅**用于备份Portainer配置。它**不会**备份您部署在环境中的内容（例如容器、堆栈、服务、卷等）。


### 备份到本地磁盘 <a href="#backup-to-local-disk" id="backup-to-local-disk"></a>

以管理员用户登录。从菜单中选择**设置**，然后滚动到**备份Portainer**部分。

<figure><img src="..//assets/2.20-settings-general-backup.gif" alt=""><figcaption></figcaption></figure>

**下载备份文件**是默认选项。作为可选步骤，切换**密码保护**开启并输入密码以加密备份文件。点击**下载备份**后，将通过浏览器下载一个`tar.gz`文件。

### 备份到S3

使用Portainer商业版，您可以选择将配置备份存储在S3存储桶中，可以按需备份或按计划备份。

要执行此操作，请以管理员用户登录，从菜单中选择**设置**，然后滚动到**备份Portainer**部分。

<figure><img src="..//assets/2.20-settings-general-backup.gif" alt=""><figcaption></figcaption></figure>

选择**存储在S3**并填写选项，参考以下指南。

| 字段/选项               | 概述                                                                                                                                                                                                                                                                                                      |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 计划自动备份 | 启用此选项以计划将配置自动备份到S3存储桶。                                                                                                                                                                                                                            |
| Cron规则                  | <p>使用<a href="https://en.wikipedia.org/wiki/Cron">cron</a>格式定义备份运行的频率。</p><p><code>[分钟] [小时] [日] [月] [星期]</code></p><p>例如，以下设置将在每周二凌晨3:41运行备份：</p><p><code>41 3 * * 2</code></p> |
| 访问密钥ID              | 输入您的S3存储桶的访问密钥ID。                                                                                                                                                                                                                                                                   |
| 秘密访问密钥          | 输入您的S3存储桶的秘密密钥。                                                                                                                                                                                                                                                                      |
| 区域                     | 输入您的存储桶所在的区域（例如`us-west-1`）。                                                                                                                                                                                                                                     |
| 存储桶名称                | 输入您的S3存储桶名称。                                                                                                                                                                                                                                                                             |
| S3兼容主机         | 如果您使用的是非AWS的S3兼容提供商（如MinIO），请在此处输入URL（包括协议和端口，如果需要）。如果使用AWS S3，请留空。                                                                                                                               |
| 密码保护           | 启用此选项以使用密码保护您的备份。                                                                                                                                                                                                                                                          |
| 密码                   | 输入要设置在备份上的密码。                                                                                                                                                                                                                                                                    |

<figure><img src="..//assets/2.17-admin-settings-backup-s3.png" alt=""><figcaption></figcaption></figure>

### 从本地文件恢复

只能在初始安装期间在新Portainer实例上恢复配置。当您需要恢复Portainer时，部署一个具有空数据卷的新Portainer实例，并在设置期间选择**从备份恢复Portainer**选项。

<figure><img src="..//assets/2.15-backup-restore-file.png" alt=""><figcaption></figcaption></figure>

在初始化页面上，展开**从备份恢复Portainer**。点击**选择文件**，然后浏览并选择`tar.gz`备份文件。如果备份最初已加密，请输入密码，然后点击**恢复Portainer**。

恢复可能需要一些时间。完成后，您将被重定向到登录页面。您现在可以使用之前的凭据登录，之前的配置将被恢复。

### 从S3恢复


此功能仅在Portainer商业版中可用。


只能在初始安装期间在新Portainer实例上恢复配置。当您需要恢复Portainer时，部署一个具有空数据卷的新Portainer实例，并在设置期间选择**从备份恢复Portainer**选项，确保选择**从S3检索**。参考下表填写各字段。

| Field/Option       | Overview                                                                                                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Access key ID      | Enter the access key ID for your S3 bucket.                                                                                                                                     |
| Secret access key  | Enter the secret key for your S3 bucket.                                                                                                                                        |
| Region             | Enter the region where your bucket is located (for example, `us-west-1`).                                                                                                       |
| Bucket name        | Enter the name of your S3 bucket.                                                                                                                                               |
| S3 Compatible Host | If you are using a non-AWS S3-compatible provider (such as MinIO), enter the URL (including the protocol and port if necessary) here. If you're using AWS S3, leave this blank. |
| Filename           | Enter the filename of the backup you want to restore.                                                                                                                           |
| Password           | Enter the password set on your backup (if any).                                                                                                                                 |

<figure><img src="..//assets/2.17-admin-settings-backup-s3-restore.png" alt=""><figcaption></figcaption></figure>

准备好后，点击**恢复Portainer**。恢复可能需要一些时间。完成后，您将被重定向到登录页面。您现在可以使用之前的凭据登录，之前的配置将被恢复。

## Portainer支持

本节包含与Portainer安装故障排除相关的设置。

### 支持包

此功能允许您收集有关Portainer安装的信息到一个包中，然后可以提供给Portainer支持团队以帮助故障排除。在生成之前，密码和其他敏感凭据等个人信息会从此包中删除。

您可以选择通过切换**密码保护**并设置密码来保护包。如果设置了密码，请确保在提供包时将密码告知Portainer支持团队。

<figure><img src="..//assets/2.25.0-settings-support-bundle.png" alt=""><figcaption></figcaption></figure>

点击**下载支持包**生成并下载包含包的`.tar.gz`文件。

### 调试日志

切换**启用调试日志**开启以在Portainer容器日志中启用调试日志记录。调试日志记录可以通过提供更详细的输出来帮助故障排除。

<figure><img src="..//assets/2.25.0-settings-support-debug.png" alt=""><figcaption></figcaption></figure>
