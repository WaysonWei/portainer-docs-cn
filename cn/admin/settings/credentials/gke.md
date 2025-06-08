# 添加Google Cloud凭据

在将Google Cloud凭据添加到Portainer之前，您需要为GKE配置账户，设置服务账户并获取该服务账户的私钥。完成后，您可以使用私钥设置访问权限。

## 创建私钥

登录Google Cloud控制台并进入项目仪表板。要确认项目已启用GKE，请点击左侧菜单中的**Kubernetes Engine**。如果该部分加载并显示创建集群的能力，则表示已设置完成。否则系统会要求您**启用Kubernetes Engine API**，您应该执行此操作。

确认后，我们需要创建一个服务账户。从导航菜单中，悬停在**IAM & Admin**上并点击**Service Accounts**，然后点击**Create Service Account**。填写服务账户详细信息，包括名称、ID和描述，然后点击**Create and Continue**。在**Grant this service account access to project**部分，为服务账户添加`Compute Engine Service Agent`和`Kubernetes Engine Service Agent`角色，点击**Continue**，然后点击**Done**创建账户。

最后，我们需要获取服务账户的私钥。点击您刚创建的服务账户，选择**Keys**选项卡，点击**Add Key**然后**Create new key**。选择**JSON**作为类型并点击**Create**。这将下载包含服务账户私钥的文件。

## 添加您的凭据

要为Google Cloud账户添加凭据，从[共享凭据](./)页面点击**添加凭据**，然后选择**Google Cloud**选项。为您的凭据集指定一个**名称**，并上传服务账户的JSON私钥。

<figure><img src="../..//assets/2.21.2-settings-cloud-credentials-googlecloud.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**添加凭据**。您的凭据现在可以在[在Google Cloud上配置Kubernetes集群](../../environments/add/kaas/gke.md)时使用。
