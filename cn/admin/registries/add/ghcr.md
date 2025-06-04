# 添加GitHub注册表

GitHub注册表选项仅在Portainer商业版中可用。

从菜单中选择**注册表**，然后点击**添加注册表**并选择**GitHub**作为注册表提供商。

<figure><img src="../..//assets/2.17-registries-add-github.gif" alt=""><figcaption></figcaption></figure>

填写表单，参考下表作为指南。

| 字段/选项              | 概述                                                                                                                                                                                                                                                                                                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 名称                  | 输入您想在Portainer中用于此注册表的名称。                                                                                                                                                                                                                                                                                                                                                  |
| 用户名                | 输入用于登录GitHub注册表的用户名。                                                                                                                                                                                                                                                                                                                                                         |
| 个人访问令牌          | <p>输入与上述用户名对应的个人访问令牌(经典)。您的个人访问令牌(经典)需要分配<code>delete:packages</code>、<code>repo</code>和<code>write:packages</code>权限范围。<br>GitHub<a href="https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-to-the-container-registry">目前不支持</a>使用细粒度令牌访问注册表。</p> |
| 使用组织注册表        | 如果您的注册表属于GitHub组织，请切换此选项。                                                                                                                                                                                                                                                                                                                                               |
| 组织名称              | 输入您的GitHub组织名称。                                                                                                                                                                                                                                                                                                                                                                   |

<figure><img src="../..//assets/2.17-registries-add-ghcr-details.png" alt=""><figcaption></figcaption></figure>

有关创建个人访问令牌的更多信息，请参阅[GitHub官方文档](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)。

表单填写完成后，点击**添加注册表**。
