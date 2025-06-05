# 初始设置

Portainer Server 部署完成后，访问实例的 URL 即可开始初始设置。

## 创建第一个用户

您的第一个用户将是管理员。用户名默认为 `admin`，但您可以根据需要更改。密码必须至少 12 个字符并满足列出的密码要求。

<figure><img src="../..//assets/2.15-install-server-setup-user.png" alt=""><figcaption></figcaption></figure>

## 启用或禁用统计收集

我们使用 [Matomo](https://matomo.org/) 工具收集有关 Portainer 使用情况的匿名信息。我们建议启用此选项，以便我们根据使用情况做出改进。有关我们如何处理收集的信息的更多详情，请阅读我们的[隐私政策](https://www.portainer.io/privacy-policy)。

在安装过程中，您可以使用复选框启用或禁用连接统计。如果您之后改变主意，可以在 Portainer UI 的[设置](../../../admin/settings/general.md#allow-the-collection-of-anonymous-statistics)中轻松更新此选项。

<figure><img src="../..//assets/2.15-install-server-setup-matomo.png" alt=""><figcaption></figcaption></figure>

## 添加许可证密钥

系统将要求您提供许可证密钥。在注册 Business Edition 或免费试用时您应该已获得此密钥。如果您没有许可证密钥，可以点击**没有许可证？**链接或[联系我们的团队](mailto:success@portainer.io)。

将提供的许可证密钥粘贴到框中，然后点击**提交**。

<figure><img src="../..//assets/2.20-initial-setup-license.png" alt=""><figcaption></figcaption></figure>

## 将 Portainer 连接到您的环境

创建管理员用户后，**环境向导**将自动启动。该向导将帮助您开始使用 Portainer。

<figure><img src="../..//assets/2.15-install-server-setup-wizard.png" alt=""><figcaption></figcaption></figure>

安装过程会自动检测您的本地环境并为您设置。如果您想添加其他环境来管理此 Portainer 实例，请点击**添加环境**。否则，点击**开始使用**即可开始使用 Portainer！
