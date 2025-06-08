# 添加Civo凭据

在将Civo凭据添加到Portainer之前，您需要从Civo获取API令牌。

## 获取API令牌

登录Civo控制面板，展开**设置**菜单。选择**个人资料**，然后选择**安全**选项卡。

在页面顶部，您应该能看到列出的API密钥。

## 添加您的凭据

要为Civo账户添加凭据，从[共享凭据](./)页面点击**添加凭据**，然后选择**Civo**选项。为您的凭据集指定一个**名称**，并将**API密钥**粘贴到框中。

<figure><img src="../..//assets/2.21.2-settings-cloud-credentials-civo.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**添加凭据**。您的凭据现在可以在[在Civo上配置Kubernetes集群](../../environments/add/kaas/civo.md)时使用。
