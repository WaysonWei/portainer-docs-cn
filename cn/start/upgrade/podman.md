# 在 Podman 上更新

始终确保 Agent 版本与 Portainer Server 版本匹配。换句话说，当您安装或更新到 Portainer 2.27.6 时，请确保所有 Agent 也都在 2.27.6 版本。

在开始任何更新之前，我们强烈建议[备份](../../admin/settings/general.md#back-up-portainer)当前的 Portainer 配置。

## 更新 Portainer Server

从 Portainer CE 2.9 和 BE 2.10 开始，默认在端口 `9443` 上启用 HTTPS。这些说明将配置 Portainer 使用 9443 进行 HTTPS 通信，并且不暴露 9000 用于 HTTP。如果需要保留 HTTP 访问，可以在命令中添加：

`-p 9000:9000`

您也可以选择在更新后[完全禁用 HTTP](https://github.com/portainer/portainer-docs/blob/2.21/admin/settings/general/README.md#force-https-only)。在使 Portainer 仅使用 HTTPS 之前，请确保所有 Agent 和 Edge Agent 都已经使用 HTTPS 与 Portainer 通信。

本文假设您使用了我们推荐的部署脚本。

要更新到最新版本的 Portainer Server，请使用以下命令停止然后移除旧版本。您的其他应用程序/容器不会被移除。

```
podman stop portainer
```

```
podman rm portainer
```

现在您已经停止并移除了旧版本的 Portainer，必须确保本地有最新版本的镜像。您可以使用 `podman pull` 命令：

```
podman pull portainer/portainer-ee:lts
```

```
podman pull portainer/portainer-ce:lts
```

最后，部署更新后的 Portainer 版本：

```
podman run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:lts
```

```
podman run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

这些 `podman run` 命令包括打开端口 `8000`，用于 Edge Agent 通信，如我们的[安装说明](../install/server/docker/linux.md)中所包含。如果不需要此端口开放，可以从命令中移除。

要提供自己的 SSL 证书，可以使用 `--sslcert` 和 `--sslkey` 标志来提供证书和密钥文件。证书文件需要是完整的链并且是 PEM 格式。例如，对于商业版：

```
podman run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:lts --sslcert /path/to/cert/portainer.crt --sslkey /path/to/cert/portainer.key
```

最新版本的 Portainer 现在将部署在您的系统上，使用先前版本的持久数据，并将 Portainer 数据库升级到新版本。

部署完成后，转到 `https://your-server-address:9443` 或 `http://your-server-address:9000` 并登录。您应该注意到更新通知已消失，版本号已更新。

## 仅更新 Agent

要更新到最新版本的 Portainer Agent，请使用以下命令停止然后移除旧版本。您的其他应用程序/容器不会被移除。

```
podman stop portainer_agent
```

```
podman rm portainer_agent
```

接下来，拉取更新后的镜像：

```
podman pull portainer/agent:lts
```

最后，使用更新后的镜像启动 Agent：

```
podman run -d -p 9001:9001 --name portainer_agent --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v /var/lib/containers/storage/volumes:/var/lib/docker/volumes portainer/agent:lts
```

如果您在 Portainer Server 实例上设置了自定义 `AGENT_SECRET`（通过在启动 Portainer Server 容器时指定 `AGENT_SECRET` 环境变量），在更新 Agent 时必须记住以相同方式（作为环境变量）显式提供相同的密钥给您的 Agent：

`-e AGENT_SECRET=yoursecret`
