# 添加AWS ECR注册表

从菜单中选择**注册表**，然后点击**添加注册表**并选择**AWS ECR**作为注册表提供商。

<figure><img src="../..//assets/2.19-registries-add-ecr.gif" alt=""><figcaption></figcaption></figure>

## 准备工作

如果您的注册表需要身份验证才能访问，您必须创建一个具有注册表访问权限的IAM用户供Portainer使用。创建IAM用户的说明可从[AWS文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console)获取。创建用户后，请记下**访问密钥ID**和**秘密访问密钥**，因为您将在下面需要这些信息。

目前我们不支持启用MFA的IAM用户。我们建议专门为Portainer创建一个禁用MFA的用户。

创建用户时，您需要附加一个或多个策略以提供注册表访问权限。为了在Portainer中获得完整的注册表管理功能，我们推荐使用`AmazonEC2ContainerRegistryFullAccess`策略。

## 添加您的注册表

填写表单，参考下表作为指南。

| 字段/选项          | 概述                                                                                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 名称               | 输入您想在Portainer中用于此注册表的名称。                                                                                                                      |
| 注册表URL          | 输入您的AWS ECR注册表URL，包括账户ID和区域。您可以在AWS控制台的Amazon Container Services、ECR、Registries下找到此信息。                                        |
| 身份验证           | 如果您的注册表需要身份验证才能访问，请启用此选项。                                                                                                              |
| AWS访问密钥        | 输入将访问AWS ECR注册表的IAM用户的访问密钥ID。                                                                                                                 |
| AWS秘密访问密钥    | 输入上述IAM用户的秘密访问密钥。                                                                                                                                 |
| 区域               | 输入您的注册表所在的区域，例如`us-west-1`。                                                                                                                    |

<figure><img src="../..//assets/2.19-registries-add-ecr.png" alt=""><figcaption></figcaption></figure>

表单填写完成后，点击**添加注册表**。
