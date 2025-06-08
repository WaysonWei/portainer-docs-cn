# 添加Azure凭据

在将Azure凭据添加到Portainer之前，您需要获取订阅ID、创建应用并获取相关租户ID和客户端ID、创建客户端密钥并获取其值，以及在资源组上设置正确的角色或权限。

## 配置Azure账户

登录Azure门户。首先点击**订阅**并记下您的**订阅ID**。

然后点击左上角菜单并选择**Azure Active Directory**。点击左侧菜单中的**应用注册**并选择**新注册**。

输入一个有意义的注册名称，其他字段保持默认。点击**注册**创建应用注册。在出现的应用页面中，记下**应用程序(客户端)ID**和**目录(租户)ID**。

接下来点击左侧菜单中的**证书和密码**。点击**新客户端密码**并输入密码名称。选择密码过期时间并点击**添加**。复制**客户端密码(值)** - 不需要密码ID。

现在需要设置权限。点击左上角菜单，然后选择**资源组**并选择您的资源组。如果没有资源组，可以创建一个新的。

点击左侧菜单中的**访问控制(IAM)**，然后点击**添加角色分配**。我们建议选择`Contributor`角色，但如果您想指定精确权限集，如下所示：

```
Microsoft.ContainerService/managedClusters/read
Microsoft.ContainerService/managedClusters/write
Microsoft.Resources/deployments/*
Microsoft.Resources/subscriptions/resourcegroups/read
Microsoft.Resources/subscriptions/resourcegroups/write
Microsoft.Resources/subscriptions/read
Microsoft.ContainerService/managedClusters/listClusterAdminCredential/action
```

选择权限后点击**下一步**。点击**选择成员**然后搜索您之前注册的应用。选中后点击页面底部的**选择**。点击**查看+分配**，然后在下一页再次点击**查看+分配**。

## 添加您的凭据

要为Azure账户添加凭据，从[云设置](./)页面点击**添加凭据**，然后选择**Microsoft Azure**选项。输入凭据**名称**，并粘贴**订阅ID**、**租户ID**、**客户端ID**和**客户端密码**。

<figure><img src="../..//assets/2.21.2-settings-cloud-credentials-azure.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**添加凭据**。您的凭据现在可以在[在Azure上配置Kubernetes集群](../../environments/add/kaas/aks.md)时使用。
