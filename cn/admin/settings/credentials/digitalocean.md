# 添加DigitalOcean凭据

在将DigitalOcean凭据添加到Portainer之前，您需要在DigitalOcean账户中创建一个API令牌。

## 创建API令牌

登录DigitalOcean控制面板，在左下角选择**API**。点击**生成新令牌**，输入令牌名称和过期时间，并确保同时勾选了**读取**和**写入**权限范围。

## 添加您的凭据

要为DigitalOcean账户添加凭据，从[共享凭据](./)页面点击**添加凭据**，然后选择**DigitalOcean**选项。为您的凭据集指定一个**名称**，并将**API密钥**粘贴到框中。

<figure><img src="../..//assets/2.21.2-settings-cloud-credentials-digitalocean.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**添加凭据**。您的凭据现在可以在[在DigitalOcean上配置Kubernetes集群](../../environments/add/kaas/digitalocean.md)时使用。
