# 账户设置

要访问和更新您的用户设置，请点击Portainer UI右上角的用户名并选择**我的账户**。

<figure><img src="/assets/2.20-api-access-myaccount.gif" alt=""><figcaption></figcaption></figure>

## 更改主题

Portainer允许您在浅色、深色和高对比度主题之间进行选择，或根据系统主题自动选择。所选主题仅适用于当前用户。

从选项中选择一个主题，更改将自动应用。

<figure><img src="/assets/2.15-accountsettings-theme.png" alt=""><figcaption></figcaption></figure>

## 更改密码

输入以下详细信息，参考下方表格作为指南。完成后点击**更新密码**。

<figure><img src="/assets/2.15-accountsettings-changepw.png" alt=""><figcaption></figcaption></figure>

| 字段/选项       | 说明                                                     |
| --------------- | -------------------------------------------------------- |
| 当前密码        | 输入您当前用于登录Portainer的密码。                      |
| 新密码          | 为您的账户输入一个新密码。                               |
| 确认密码        | 再次输入新密码。                                         |

[最小密码长度要求](../admin/settings/authentication/)由管理员设置。

## 应用设置

在本部分，您可以启用或禁用Kubernetes环境的前端数据缓存。启用此选项后，Portainer会缓存前端提供的Kubernetes集群数据以提高查看集群时的加载速度。但这种缓存可能意味着您看到的信息可能不是完全最新的，其他用户或在Portainer之外所做的更改可能需要最多五分钟才能在您的会话中更新。

<figure><img src="/assets/2.20-account-application.png" alt=""><figcaption></figcaption></figure>

## 访问令牌

本部分允许您管理API访问令牌。您可以查看当前用户的访问令牌列表，并根据需要添加或删除令牌。

<figure><img src="/assets/2.15-accountsettings-apitokens.png" alt=""><figcaption></figcaption></figure>

有关访问令牌的更多信息，请参阅我们的[API访问文档](../api/access.md#creating-an-access-token)。

## Git凭据

本部分允许您管理部署中使用的保存的Git凭据。这些凭据仅对您的用户可用。


此功能仅在Portainer商业版中可用。


<figure><img src="/assets/2.16-account-gitcreds.png" alt=""><figcaption></figcaption></figure>

要添加新凭据，点击**添加Git凭据**按钮并填写字段，参考下方表格作为指南：

| 字段                 | 说明                                                                                                     |
| --------------------- | -------------------------------------------------------------------------------------------------------- |
| 名称                  | 输入此凭据条目的名称。这将是在部署时选择使用它的显示方式。                                               |
| 用户名                | 输入用户名（如适用）。                                                                                   |
| 个人访问令牌          | 输入个人访问令牌。                                                                                       |

<figure><img src="/assets/2.16-account-gitcreds-add.png" alt=""><figcaption></figcaption></figure>

输入相关详细信息后，点击**保存Git凭据**以保存条目。

## Helm仓库

默认情况下，Portainer已预配置[Bitnami Helm chart仓库](https://bitnami.com/stacks/helm)。在本部分您可以添加额外的Helm仓库以便在部署Helm chart时引用。

<figure><img src="/assets/2.20-account-helmrepos.png" alt=""><figcaption></figcaption></figure>

如需添加额外的第三方仓库，点击**添加Helm仓库**，输入仓库URL并点击**保存Helm仓库**。


此处添加的仓库仅对您的用户可用。您可以在[设置](../admin/settings/general.md#helm-repository)中配置对所有用户可用的Helm仓库。


<figure><img src="/assets/2.20-account-helmrepos-add.png" alt=""><figcaption></figcaption></figure>
