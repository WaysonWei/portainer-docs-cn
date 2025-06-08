# 添加Sidero Omni凭据

在将Sidero Omni凭据添加到Portainer之前，您需要在Omni中创建一个服务账户供Portainer使用。您可以通过Omni网页界面或使用`omnictl`命令行工具来完成此操作。

## 通过Omni网页界面创建服务账户

要通过Omni网页界面为Portainer创建服务账户，首先使用管理员用户登录网页界面。登录后，点击**设置**，然后选择**服务账户**选项卡。

<figure><img src="../..//assets/2.26-settings-credentials-omni-service-webui-1.png" alt=""><figcaption></figcaption></figure>

接下来点击**创建服务账户**按钮，并按照下表填写字段：

| 字段/选项       | 概述                                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------- |
| ID              | 输入服务账户的ID。建议使用类似`portainer`的名称。                                         |
| 过期天数        | 设置服务账户的有效天数。                                                |
| 角色            | 从下拉菜单中选择`Admin`角色。Portainer需要管理员权限来创建和管理集群。 |

<figure><img src="../..//assets/2.26-settings-credentials-omni-service-webui-2.png" alt=""><figcaption></figcaption></figure>

填写完所有详细信息后，点击**创建服务账户**按钮。服务账户将被创建，并显示**服务账户密钥**。请记下此密钥，因为它不会再次显示。

<figure><img src="../..//assets/2.26-settings-credentials-omni-service-webui-3.png" alt=""><figcaption></figcaption></figure>

现在您可以继续[添加您的凭据](omni.md#添加您的凭据)。

## 使用omnictl创建服务账户

要使用`omnictl`为Portainer创建服务账户，您首先需要一个安装了`omnictl`并配置为使用管理员用户连接到Omni安装的环境。您可以从[Sidero Omni文档](https://omni.siderolabs.com/how-to-guides/install-and-configure-omnictl)了解更多信息。

安装并配置好`omnictl`后，可以运行以下命令创建服务账户：

```
onictl serviceaccount create portainer
```

这将创建一个名为`portainer`的服务账户，有效期为1年，并具有与创建它的用户相同的角色。该命令将输出`OMNI_ENDPOINT`和`OMNI_SERVICE_ACCOUNT_KEY`值 - 请记下这两个值，因为在下一步中您将需要它们。

现在您可以继续[添加您的凭据](omni.md#添加您的凭据)。

## 添加您的凭据

要为Omni账户添加凭据，从[共享凭据](./)页面点击**添加凭据**，然后选择**Sidero Omni**选项。为您的凭据集指定一个**名称**，并将**端点URL**和**服务账户密钥**粘贴到相应的框中。

<figure><img src="../..//assets/2.26-settings-credentials-omni-add.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**添加凭据**。您的凭据现在可以在[创建Omni Talos集群](../../environments/add/kube-create/omni.md)时使用。
