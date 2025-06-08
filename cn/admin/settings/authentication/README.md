# 认证

Portainer提供内置的认证机制，对用户密码进行加密并存储在本地Portainer数据库中。此外，也支持外部认证提供商。本节将介绍如何通过LDAP、Active Directory和OAuth进行认证。

对于所有认证类型，您可以调整会话有效期（用户需要重新认证前的时长）。默认值为8小时。

使用内部认证时，管理员可以设置用户密码的最小长度。默认值为12个字符，但可以通过滑块进行调整。密码不符合要求的用户将在下次登录时被要求更新密码。

<figure><img src="../..//assets/2.15-settings-authentication.png" alt=""><figcaption></figcaption></figure>


[ldap.md](ldap.md)



[active-directory.md](active-directory.md)



[oauth.md](oauth.md)
