# Authentication

Portainer provides its own internal authentication mechanism, encrypting user passwords and storing them in the local Portainer database. Alternatively, external authentication providers are available. In this section, we explain how to authenticate via LDAP, Active Directory and OAuth.


For all authentication types you can adjust the session lifetime (the time before users are forced to reauthenticate). The default is 8 hours.


When using internal authentication, an administrator can set the minimum length for users' passwords. The default is 12 characters, but this can be adjusted using the slider. Any users with passwords that don't meet the requirements will be asked to update their passwords when they next log in.

<figure><img src="../..//assets/2.15-settings-authentication.png" alt=""><figcaption></figcaption></figure>


[ldap.md](ldap.md)



[active-directory.md](active-directory.md)



[oauth.md](oauth.md)




