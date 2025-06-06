# Docker Swarm

本文假设您使用了我们推荐的部署脚本。

在开始之前，请从我们发送的电子邮件中复制许可证密钥。

要将 Docker Swarm 升级到 Portainer 商业版，使用以下命令在您的 Swarm 集群上部署最新版本的 Portainer 商业版：

```
docker service update --image portainer/portainer-ee:lts --force portainer_portainer
```

退出 Portainer（如果当前已登录）然后重新登录。当您首次登录时，系统会要求您输入许可证密钥。从我们发送的电子邮件中粘贴此密钥。

<figure><img src="../..//assets/2.20-initial-setup-license.png" alt=""><figcaption></figcaption></figure>

左下角现在会显示"Business Edition"。
