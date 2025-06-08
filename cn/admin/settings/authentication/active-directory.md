# 通过Active Directory认证

Portainer商业版允许您连接到现有的Microsoft Active Directory服务来管理Portainer中的认证设置。

要设置Active Directory认证，从菜单中选择**设置**，然后选择**认证**。在**认证方法**部分选择**Microsoft Active Directory**。

<figure><img src="../..//assets/2.15-settings-authentication-ad.gif" alt=""><figcaption></figcaption></figure>

以下是所有Active Directory配置设置的指南。

## 自动用户配置

启用此设置后，一旦用户通过Active Directory(AD)成功认证，Portainer将自动创建用户。如果不启用此功能，您必须[手动创建用户](ldap.md#manually-creating-ldap-users)，用户名需与对应的AD用户相同。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-auto.png" alt=""><figcaption></figcaption></figure>

## AD配置

使用下表作为指南配置您的Active Directory详情。

| 字段/选项             | 概述                                                                                                                                                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| AD控制器            | 输入域控制器的FQDN或IP地址。如果需要添加多个服务器，点击**添加额外服务器**。                                                                                        |
| 服务账户          | 输入用于连接Active Directory并搜索用户的账户名称。                                                                                                                                     |
| 服务账户密码 | 输入上述服务账户的密码。                                                                                                                                                                        |
| 连接性检查       | 执行检查以确保Portainer与您的Active Directory服务器之间存在连接性和SSL握手（如果在**AD连接安全性**部分选择了**使用StartTLS**或**使用TLS**）。 |

<figure><img src="../..//assets/2.15-settings-authentication-ad-config.png" alt=""><figcaption></figcaption></figure>

## AD连接安全性

使用下表作为指南配置安全设置。

| 字段/选项                            | 概述                                                                                                                                                  |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 使用StartTLS                            | 启用此选项以使用StartTLS保护与服务器的连接。启用后将隐藏并忽略**使用TLS**选项。             |
| 使用TLS                                 | 如果需要指定TLS证书连接LDAP服务器，请启用此选项。启用后将隐藏并忽略**使用StartTLS**选项。 |
| 跳过服务器证书验证 | 切换此选项以跳过服务器TLS证书验证。不建议在不安全的网络上使用。                          |
| TLS CA证书                      | 允许您上传TLS证书的CA证书。                                                                                              |

<figure><img src="../..//assets/2.15-settings-authentication-ad-security.png" alt=""><figcaption></figcaption></figure>

## 用户搜索配置

使用下表作为指南配置用户搜索设置。点击**添加用户搜索配置**可设置多个配置。

| 字段/选项                | 概述                                                                                                                          |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| 用户名格式             | 选择登录Portainer时使用的用户名格式。选项为`username`和`username@domainname`。         |
| 根域                 | 将自动填充域控制器的域。                                                                     |
| 用户搜索路径(可选) | 点击**添加其他条目**定义搜索用户的特定OU或文件夹。                                                |
| 允许的组(可选)   | 点击**添加其他组**定义允许访问Portainer的特定组。                                          |
| 用户过滤器                 | 将根据您之前选择的选项自动填充。                                                                 |
| 显示用户               | 点击此按钮使用提供的设置查询Active Directory服务器，获取匹配指定条件的用户列表。 |

<figure><img src="../..//assets/2.15-settings-authentication-ad-usersearch.png" alt=""><figcaption></figcaption></figure>

## 组搜索配置

使用下表作为指南配置组搜索设置。点击**添加组搜索配置**可设置多个配置。

| 字段/选项                 | 概述                                                                                                                                                                     |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 组搜索路径(可选) | 点击**添加其他条目**定义搜索组的特定OU或文件夹。                                                                                          |
| 组Base DN                | 根据之前的选择自动更新。                                                                                                                          |
| 组                       | 点击**添加其他组**通过OU或文件夹名称定义特定组。                                                                                                  |
| 组过滤器                 | 将根据之前选择的选项自动填充。                                                                                                                    |
| 显示用户/组匹配  | 点击此按钮使用Portainer中提供的设置查询Active Directory服务器，获取匹配指定条件的用户列表及其与组的匹配情况。 |

<figure><img src="../..//assets/2.15-settings-authentication-ad-groupsearch.png" alt=""><figcaption></figcaption></figure>

## 自动填充团队管理员

如果需要，Portainer可以配置指定的AD用户组自动成为Portainer管理员。

要配置此功能，首先点击**添加组搜索配置**并根据需要定义**组Base DN**、**组**和**组过滤器**。完成后，点击**获取管理员组**按钮检索匹配搜索配置的组列表。

<figure><img src="../..//assets/2.15-settings-authentication-ad-autopop.png" alt=""><figcaption></figcaption></figure>

当您对组选择满意后，通过切换**为组分配管理员权限**来启用此功能。

## 测试登录

要测试您的设置是否正确以及是否配置了正确的用户和组进行访问，滚动到**测试登录**，输入有效的用户和密码，然后点击**测试**。如果一切正常，按钮旁边会出现一个绿色勾号。

<figure><img src="../..//assets/2.15-settings-authentication-ad-testlogin.png" alt=""><figcaption></figcaption></figure>
