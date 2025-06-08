# 添加Akamai Connected Cloud凭据

在将Akamai Connected Cloud凭据添加到Portainer之前，您需要在Akamai账户中创建一个API令牌。

## 创建API令牌

登录Akamai控制面板，点击右上角的账户名称。选择**API令牌**。点击**创建个人访问令牌**，为其指定标签并设置有效期。Portainer配置功能仅需要**Kubernetes**选项的**读/写**权限，因此可以禁用其他权限。

## 添加您的凭据

要为Akamai账户添加凭据，从[共享凭据](./)页面点击**添加凭据**，然后选择**Akamai Connected Cloud**选项。为您的凭据集指定一个**名称**，并将**API密钥**粘贴到框中。

<figure><img src="../..//assets/2.21.2-settings-cloud-credentials-akamai.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**添加凭据**。您的凭据现在可以在[在Akamai Connected Cloud上配置Kubernetes集群](../../environments/add/kaas/linode.md)时使用。
