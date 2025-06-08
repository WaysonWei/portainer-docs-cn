# 通过LDAP认证

## 简介

如果您的组织已实现LDAP认证，可以配置Portainer接受轻量级目录访问协议(LDAP)认证。当用户尝试登录Portainer时，应用程序将根据您的LDAP目录进行认证。如果认证成功，用户将被允许登录Portainer。

要配置Portainer LDAP认证，首先需要为Portainer读取LDAP添加一个目录服务用户。该用户应是一个服务账户，仅需要LDAP的只读访问权限。

## 启用LDAP

以管理员身份登录Portainer。从菜单中选择**设置**，选择**认证**，然后选择**LDAP认证**选项。将显示额外字段，允许您配置LDAP。

<figure><img src="../..//assets/2.15-settings-authentication-ldap.gif" alt=""><figcaption></figcaption></figure>

### 自动用户配置

启用此设置后，一旦用户通过LDAP成功认证，Portainer将自动创建用户。如果不启用此功能，您必须[手动创建用户](ldap.md#manually-creating-ldap-users)，用户名需与对应的LDAP目录中的用户名相同。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-auto.png" alt=""><figcaption></figcaption></figure>

### 服务器类型

在此处您可以选择自定义配置或预配置的OpenLDAP模板。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-type.png" alt=""><figcaption></figcaption></figure>

### LDAP配置

输入LDAP服务器的IP地址/FQDN和端口号。选择匿名连接（您的LDAP服务器必须支持此功能）或输入具有目录READ访问权限的用户账户。点击**测试连接**以验证是否可以连接。

对于OpenLDAP，Reader DN格式应设置为`cn=user,dc=domain,dc=tld`。如果您的配置不同，需要相应调整此格式。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-config.png" alt=""><figcaption></figcaption></figure>

如果需要添加额外的LDAP服务器以提供认证回退，点击**添加额外服务器**并填写服务器详情。

### LDAP安全

配置剩余的LDAP设置，参考下表作为指南：

| 字段/选项                            | 概述                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 使用StartTLS                            | 在初始连接后将不安全连接更改为安全连接。                                                                                                                                                                                                                                                                    |
| 使用TLS                                 | 使用TLS初始化与LDAP的连接。                                                                                                                                                                                                                                                                                                  |
| 跳过服务器证书验证 | 如果无法访问LDAP服务器证书，跳过验证将启用加密通信。但您必须手动确保正在与URL中指定的目标LDAP服务器通信。如果被恶意重定向，您可能正在与不同的服务器通信。请谨慎使用。 |

<figure><img src="../..//assets/2.15-settings-authentication-ldap-security.png" alt=""><figcaption></figcaption></figure>

| 字段/选项       | 概述                                                       |
| ------------------ | -------------------------------------------------------------- |
| TLS CA证书 | 允许您上传用于安全连接的CA证书。 |

<figure><img src="../..//assets/2.15-settings-authentication-ldap-security-tls.png" alt=""><figcaption></figcaption></figure>

### 用户搜索配置

#### BaseDN

* 输入 `dc=mydomain,dc=com` 在整个目录中搜索尝试登录的用户名
* 输入 `ou=myou,dc=mydomain,dc=com` 仅在指定的OU中搜索用户
* 如果您的用户仅在一个容器中，输入 `cn=mycn,dc=mydomain,dc=com`

如果您的域中有大量用户，可以通过使用OU来缩小Portainer的搜索范围。

#### 用户名属性

对于LDAP，除非您的配置不同，否则输入 `uid`。

#### 过滤器

这些条目区分大小写。

输入从LDAP返回结果到Portainer的过滤条件。例如，要仅允许属于OU中定义的组成员的用户登录，将**过滤器**设置为以下内容（括号很重要，请复制整个字符串）：

```
(&(objectClass=user)(memberOf=cn=mycn,ou=myou,dc=mydomain,dc=com))
```

在下面的示例中，域 `portainer.local` 有一个名为 `Groups` 的OU，其中包含一个名为 `PortainerDevUsers` 的组。此搜索过滤器将仅允许属于 `PortainerDevUsers` LDAP组的用户登录Portainer。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-usersearch.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，点击**添加用户搜索配置**以定义额外的用户搜索配置。

### 组搜索配置

除了用户搜索外，Portainer还允许您设置组搜索。配置后，如果LDAP用户是LDAP组的成员，并且该LDAP组对应同名的Portainer[团队](../../user/teams/)，则LDAP用户将根据其LDAP组成员资格自动加入Portainer团队。这对于通过组成员资格自动授予Portainer环境访问权限非常有用。

#### 组Base DN

输入以下之一：
* 输入 `dc=mydomain,dc=com` 在整个目录中搜索组列表
* 输入 `ou=myou,dc=mydomain,dc=com` 仅在指定的OU中搜索组
* 如果您的组仅在一个容器中，输入 `cn=mycn,dc=mydomain,dc=com`

如果您的域中有大量组，可以通过使用OU来缩小Portainer的搜索范围。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-groupsearch.png" alt=""><figcaption></figcaption></figure>

#### 组成员属性

输入 `member` 作为确定用户是否为组成员的属性。

#### 组过滤器

如果要过滤组列表仅返回包含字符串 `Portainer` 的组（例如：`PortainerDev`、`PortainerProd`、`PortainerUAT`），请按如下方式设置过滤器：

```
(&(objectclass=group)(cn=*Portainer*))
```

<figure><img src="../..//assets/2.15-settings-authentication-ldap-groupsearch-filter.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，点击**添加组搜索配置**以定义额外的组搜索配置。

### 自动填充团队管理员

如果需要，Portainer可以配置指定的LDAP用户组自动成为Portainer管理员。

要配置此功能，首先点击**添加组搜索配置**并根据需要定义**组Base DN**、**组**和**组过滤器**。完成后，点击**获取管理员组**按钮检索匹配搜索配置的组列表。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-autopop.png" alt=""><figcaption></figcaption></figure>

当您对组选择满意后，通过切换**为组分配管理员权限**来启用此功能。

### 测试登录

要测试您的配置，可以输入用户名和密码并点击**测试**按钮。

<figure><img src="../..//assets/2.15-settings-authentication-ldap-testlogin.png" alt=""><figcaption></figcaption></figure>

## 手动创建LDAP用户

这是一个可选步骤，仅在您不使用自动用户配置时才需要。

启用LDAP后，从菜单中选择**用户**。创建一个用户名，该用户名需与LDAP源用户匹配，格式与启用LDAP时定义的格式相同（`username`或`username@mydomain.com`）。
