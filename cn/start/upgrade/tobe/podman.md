# Podman

本文假设您使用了我们推荐的部署脚本。

在开始之前，请从我们发送的电子邮件中复制许可证密钥。

要将 Podman 升级到 Portainer 商业版，使用以下命令停止然后移除旧版本。您的其他应用程序/容器不会被移除。

```
podman stop portainer
podman rm portainer
```

现在您已经停止并移除了旧版本的 Portainer，运行此命令部署最新版本的 Portainer 商业版：

```
podman run -d -p 8000:8000 -p 9000:9000 -p 9443:9443 --name=portainer --restart=always --pull=always --privileged -v /run/podman/podman.sock:/run/podman/podman.sock -v portainer_data:/data portainer/portainer-ee:lts
```

退出 Portainer（如果当前已登录）然后重新登录。当您首次登录时，系统会要求您输入许可证密钥。从我们发送的电子邮件中粘贴此密钥。

<figure><img src="../..//assets/2.20-initial-setup-license.png" alt=""><figcaption></figcaption></figure>

左下角现在会显示"Business Edition"。
