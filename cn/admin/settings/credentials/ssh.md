# 添加SSH凭据

SSH凭据目前被Portainer用于Kubernetes配置功能。任何管理员级别的用户都可以使用这些凭据，但他们无法直接查看实际的凭据内容。

## 设置SSH用户

配置SSH用户的具体方法因平台而异。对于Kubernetes配置功能，我们对您创建的用户有以下假设：

* 用户具有sudo权限或是root用户 - 因为Portainer需要此级别权限来安装Kubernetes
* SSH在服务器的22端口监听

我们通常建议使用SSH密钥认证而非密码认证，但Portainer同时支持两种方法。

## 添加您的凭据

要添加SSH凭据，从[共享凭据](./)页面点击**添加凭据**，然后选择**SSH**选项。填写以下相关字段：

| 字段/选项               | 概述                                                                                                             |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| 凭据名称           | 输入用于在Portainer中识别凭据集的名称                              |
| SSH用户名               | 输入SSH账户的用户名                                                                             |
| SSH密码               | 输入SSH账户的密码。如果使用SSH密钥认证，可留空此字段 |
| 使用SSH密钥认证 | 启用此选项以使用SSH密钥认证而非密码认证                                 |
| SSH私钥密码 | 如果SSH私钥已加密，请在此提供密码                                                   |
| SSH私钥            | 在此字段粘贴您的SSH私钥                                                                            |

<figure><img src="../..//assets/2.21.2-settings-cloud-credentials-ssh.png" alt=""><figcaption></figcaption></figure>

您也可以点击**上传SSH私钥**并选择文件来上传私钥。这将用上传文件的内容替换SSH私钥字段中的任何内容。

准备就绪后，点击**添加凭据**完成流程。

### 生成新密钥对

如需为SSH凭据创建新密钥对，可点击**生成新的RSA SSH密钥对**。首先会提示您输入私钥的可选密码，然后点击**生成SSH密钥对**按钮继续。

<figure><img src="../..//assets/2.18-settings-credentials-ssh-generate-1.png" alt=""><figcaption></figcaption></figure>

Portainer将为您生成新密钥对并显示生成的私钥和公钥。您可以使用复制按钮将值复制到剪贴板，或使用下载按钮下载单个文件。

请确保复制公钥和私钥，因为之后将无法检索它们。

<figure><img src="../..//assets/2.18-settings-credentials-ssh-generate-2.png" alt=""><figcaption></figcaption></figure>

新生成的公钥应添加到您计划用于节点配置的SSH用户的`authorized_keys`文件中。

密钥对使用`4096`位密钥大小生成。

保存公钥和私钥文件后，点击**继续**。您将返回上一屏幕，SSH私钥密码和SSH私钥字段将分别填充新密钥对的密码和私钥。
