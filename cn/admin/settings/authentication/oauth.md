# 通过OAuth认证

## 在Portainer中配置OAuth认证

从菜单中选择**设置**，然后选择**认证**。在**认证方法**部分点击**OAuth**。

<figure><img src="../..//assets/2.15-settings-authentication-oauth.gif" alt=""><figcaption></figcaption></figure>

在下一个屏幕中，使用下表作为指南输入OAuth提供商提供的凭据。

| 字段/选项                        | 概述                                                                                                                                                                                                                                                                                          |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 使用SSO                             | 启用SSO后，当用户处于当前登录会话时，OAuth提供商将不会强制要求输入凭据。                                                                                                                                                                       |
| 隐藏内部认证提示 | 隐藏通过内部认证登录的能力。请注意，当启用外部认证时，[只有初始管理员用户](https://portal.portainer.io/knowledge/can-i-use-internal-authentication-and-external-authentication-at-the-same-time)可以使用内部认证登录。 |
| 自动用户配置         | 如果切换为开启，OAuth提供商端的用户将自动在Portainer中创建（您可以在此选项开启时定义默认团队来放置这些用户）。如果切换为关闭，您需要[手动在Portainer中创建用户](../../user/add.md)。                      |

<figure><img src="../..//assets/2.15-settings-authentication-oauth-sso.png" alt=""><figcaption></figcaption></figure>

如果切换**自动团队成员资格**为开启，您可以选择基于**声明名称**自动将OAuth用户添加到特定Portainer团队。声明名称将与团队匹配，或者您可以在**静态分配团队**选项下手动将声明名称（使用正则表达式）与Portainer团队关联。您还可以为不属于任何其他团队的用户定义**默认团队**。

此外，如果需要，您可以启用对指定组自动分配管理员权限。

<figure><img src="../..//assets/2.15-settings-authentication-oauth-team.png" alt=""><figcaption></figcaption></figure>

当配置Microsoft Entra ID (Azure AD)作为OAuth提供商时，您需要[使用组的Object Id值](https://learn.microsoft.com/en-us/entra/fundamentals/how-to-manage-groups#edit-group-settings)作为声明值的正则表达式，而不是组名：

<figure><img src="../..//assets/2.20-settings-authentication-oauth-ad-teammembership-objectid.png" alt=""><figcaption></figcaption></figure>

## OAuth提供商

Portainer提供预配置的OAuth提供商选项，或者您可以设置自己的自定义OAuth提供商。如果需要修改Portainer默认设置，每个预配置的提供商都可以覆盖其配置。

### Microsoft

使用下表作为指南配置您的OAuth提供商。

| 字段/选项    | 概述                                                                                                          |
| --------------- | ----------------------------------------------------------------------------------------------------------------- |
| 租户ID       | 输入您要认证的Azure Directory ID。这也被称为**目录ID**。 |
| 应用ID  | 输入OAuth应用的公共标识符。                                                             |
| 应用密钥 | 输入OAuth应用的密钥。                                                                   |

您可以按照以下步骤查找这些详细信息：

1. 以管理员身份登录到您的Azure门户。

    <figure><img src="../..//assets/authentication-oauth-ms-1.png" alt=""><figcaption></figcaption></figure>

2. 点击**Azure Active Directory**然后点击**概述**。您的**租户ID**可以在右侧面板中找到。将此作为Portainer中的**租户ID**使用。

    <figure><img src="../..//assets/2.17-AzureOauth-AD.png" alt=""><figcaption></figcaption></figure>

3. 仍在Azure Active Directory中，点击**应用注册**然后点击**新注册**。

    为Portainer实例输入一个友好的名称。为支持的帐户类型选择适当的选项，为**重定向URI**选择`Web`类型，并输入您的Portainer实例监听的FQDN或IP地址`例如：https://portainer.example.com:9443`。然后点击**注册**。

    <figure><img src="../..//assets/2.17-AzureOauth-NewReg-S1.png" alt=""><figcaption></figcaption></figure>
    <figure><img src="../..//assets/2.17-AzureOauth-NewReg.png" alt=""><figcaption></figcaption></figure>

4. 创建注册后，将显示以下屏幕。使用提供的**应用ID**作为Portainer中相应字段的值。

    <figure><img src="../..//assets/2.17-AzureOauth-NewReg-S2.png" alt=""><figcaption></figcaption></figure>

5. 点击**证书和密码**然后点击**客户端密码**，点击**新客户端密码**。添加**描述**并选择过期日期，然后点击**添加**。

    随后将为您生成密钥。使用该值作为Portainer中相应字段的**应用密钥**。

    <figure><img src="../..//assets/2.17-AzureOauth-NewReg-S4.png" alt=""><figcaption></figcaption></figure>
    <figure><img src="../..//assets/2.17-AzureOauth-NewReg-S3.png" alt=""><figcaption></figcaption></figure>

6. 点击**API权限**和**添加权限**。在**请求API权限屏幕**中选择**Microsoft Graph**。选择**委派权限**并添加`email, openid, profile`权限。

    <figure><img src="../..//assets/2.17-AzureOauth-NewReg-S5.gif" alt=""><figcaption></figcaption></figure>

7. 确保您为目录授予管理员同意。

    <figure><img src="../..//assets/2.20-settings-authentication-oauth-ad-directory.png" alt=""><figcaption></figcaption></figure>

8. 可选地，要在Portainer中使用**自动团队成员资格**功能，您需要创建组声明。点击**令牌配置**和**添加组声明**。选择**安全组**并点击**添加**。

    <figure><img src="../..//assets/2.17-AzureOauth-NewReg-S6.gif" alt=""><figcaption></figcaption></figure>

<figure><img src="../..//assets/2.15-settings-authentication-oauth-ms.png" alt=""><figcaption></figcaption></figure>

完成后，点击**保存设置**。

### Google

使用下表作为指南配置您的OAuth提供商。

| 字段/选项  | 概述                                              |
| ------------- | ----------------------------------------------------- |
| 客户端ID     | 输入OAuth应用的公共标识符。 |
| 客户端密钥 | 输入OAuth应用的密钥。       |

<figure><img src="../..//assets/2.15-settings-authentication-oauth-google.png" alt=""><figcaption></figcaption></figure>

完成后，点击**保存设置**。

### Github

使用下表作为指南配置您的OAuth提供商。

| 字段/选项  | 概述                                              |
| ------------- | ----------------------------------------------------- |
| 客户端ID     | 输入OAuth应用的公共标识符。 |
| 客户端密钥 | 输入OAuth应用的密钥。       |

<figure><img src="../..//assets/2.15-settings-authentication-oauth-github.png" alt=""><figcaption></figcaption></figure>

完成后，点击**保存设置**。

### 自定义

根据下表完成**OAuth配置**部分。

| 字段/选项      | 概述                                                                                                                                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 客户端ID         | 输入OAuth应用的公共标识符。                                                                                                                                            |
| 客户端密钥     | 输入OAuth应用的令牌访问密钥。                                                                                                                                                 |
| 授权URL | 输入用于对OAuth提供商进行认证的URL（将重定向用户到OAuth提供商登录界面）。                                                                          |
| 访问令牌URL  | 输入用于将有效的OAuth认证代码交换为访问令牌的URL。                                                                                                            |
| 资源URL      | 输入Portainer用于检索认证用户信息的URL。                                                                                                               |
| 重定向URL      | 输入OAuth提供商在用户成功认证后用于重定向用户的URL（也称为回调URL）。您应将其设置为您的Portainer实例URL。 |
| 登出URL        | 输入OAuth提供商用于注销用户的URL。                                                                                                                                       |
| 用户标识符   | 输入Portainer将用于为认证用户创建帐户的标识符。从**资源URL**字段中指定的资源服务器检索。                             |
| 范围            | OAuth提供商需要这些范围来检索认证用户的信息。请参阅您提供商的文档以获取更多信息。                                                    |
| 认证风格        | 指定如何将客户端ID和客户端密钥发送到OAuth提供商。                                                                                                                       |

<figure><img src="../..//assets/2.21-settings-authentication-oauth-custom.png" alt=""><figcaption></figcaption></figure>

When you're finished, click **Save settings**.

## 为OAuth团队和用户授予环境访问权限

参见[管理用户对环境访问权限](../../environments/access.md)。
