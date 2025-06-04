# 添加Gitlab注册表

从菜单中选择**注册表**，然后点击**添加注册表**并选择**Gitlab**作为注册表提供商。

<figure><img src="../..//assets/2.15-settings-registries-add-gitlab.gif" alt=""><figcaption></figcaption></figure>

填写表单，参考下表作为指南。

| 字段/选项                   | 概述                                                                                                                         |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| 用户名                     | 输入用于登录Gitlab注册表的用户名。                                                                                          |
| 个人访问令牌               | 输入与上述用户名对应的个人访问令牌。您的个人访问令牌需要分配`read_api`和`read_registry`权限范围。                           |
| 覆盖默认配置               | 如果需要更改Portainer对Gitlab的默认配置，可以在此处进行修改。                                                              |

<figure><img src="../..//assets/2.15-settings-registries-add-gitlab-details.png" alt=""><figcaption></figcaption></figure>

有关创建个人访问令牌的更多信息，请参阅[Gitlab官方文档](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)。

表单填写完成后，点击**添加注册表**。
