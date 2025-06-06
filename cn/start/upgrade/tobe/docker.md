# Docker 单机版

本文假设您使用了我们推荐的部署脚本。

在开始之前，请从我们发送的电子邮件中复制许可证密钥。

切换到 Portainer 商业版的过程很简单，但取决于您当前运行的 Portainer 版本。从适用于您当前版本的说明开始，然后逐步向下操作。

* [版本 1.24.0 或更旧](docker.md#upgrading-from-versions-older-than-1.24.1)
* [版本 1.24.1 或 1.24.2](docker.md#upgrading-from-1.24.1-and-1.24.2)
* [版本 2.0.0 或更新](docker.md#upgrading-from-version-2.0.0-and-later)

## **从 1.24.1 之前的版本升级**

如果您运行的版本早于 1.24.1，必须首先升级到 `portainer/portainer:1.24.2`。您的其他应用程序/容器不会被移除。使用以下命令停止然后移除旧版本，然后运行 Portainer 1.24.2 版本：

```
docker stop portainer

docker rm portainer

docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer:1.24.2
```

通过登录 Portainer 并读取 UI 左下角的版本号来验证您是否正在运行 1.24.2 版本。您现在应该继续[更新到 2.0.0 版本](docker.md#upgrading-from-1.24.1-and-1.24.2)。

## 从 1.24.1 和 1.24.2 升级

如果您运行的版本早于 1.24.1 并希望更新到最新版本的 Portainer，必须首先升级到 `portainer/portainer-ce:2.0.0`，使用以下命令停止然后移除旧版本。您的其他应用程序/容器不会被移除。

```
docker stop portainer
```

```
docker rm portainer
```

现在您已经停止并移除了旧版本的 Portainer，必须确保本地有 2.0.0 版本的最新镜像。您可以使用 `docker pull` 命令：

```
docker pull portainer/portainer-ce:2.0.0
```

最后，部署更新后的 Portainer 版本：

```
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.0.0
```

Portainer CE 2.0.0 现在将部署在您的系统上，使用先前版本的持久数据，并将 Portainer 数据库升级到新版本。

部署完成后，转到 `http://your-server-address:9000` 并登录。通过登录 Portainer 并读取 UI 左下角的版本号来验证您是否正在运行 2.0.0 版本。您现在可以[升级到最新版本](docker.md#upgrading-from-version-2.0.0-and-later)的 Portainer 商业版。

## 从 2.0.0 及更高版本升级

要将 Docker 单机版升级到 Portainer 商业版，使用以下命令停止然后移除旧版本。您的其他应用程序/容器不会被移除。

```
docker stop portainer
docker rm portainer
```

现在您已经停止并移除了旧版本的 Portainer，运行此命令部署最新版本的 Portainer 商业版：

```
docker run -d -p 8000:8000 -p 9000:9000 -p 9443:9443 --name=portainer --restart=always --pull=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:lts
```

退出 Portainer（如果当前已登录）然后重新登录。当您首次登录时，系统会要求您输入许可证密钥。从我们发送的电子邮件中粘贴此密钥。

<figure><img src="../..//assets/2.20-initial-setup-license.png" alt=""><figcaption></figcaption></figure>

左下角现在会显示"Business Edition"。
