# 添加ACI环境

在连接到您的Azure订阅之前，您需要创建一个Azure AD应用程序。有关此操作的更多信息，请参阅[Microsoft官方文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal)。

当前不支持以下ACI功能：

* ACI持久存储
* 私有网络

要添加ACI环境，从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

选择**ACI**作为您的环境类型并点击**开始向导**。使用下表作为指南输入**环境详细信息**。

| 字段               | 概述                                                                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 名称               | 为您的环境输入一个名称。                                                                                                                      |
| 应用程序ID         | 输入您在Azure账户中创建的应用程序ID。这可以在Azure门户中您的应用程序的**概览**页面上找到。 |
| 租户ID             | 输入您的应用程序的租户ID。这可以在Azure门户中您的应用程序的**概览**页面上找到。                                       |
| 认证密钥           | 输入您的应用程序的客户端密钥。这可以在Azure门户中您的应用程序的**证书和密码**下创建。                 |

<figure><img src="../..//assets/2.15-aci_env.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分，通过将环境添加到[组](../groups.md)或[标记](../tags.md)来分类环境以提高可搜索性。

<figure><img src="../..//assets/2.15-aci_more-settings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
