# 从 Portainer 1.x 版本更新

如果您正在更新当前运行 1.x 系列镜像的 Portainer 安装，在更新到最新版本之前必须采取额外的步骤。本文档根据您当前的版本介绍步骤 - 从适用于您当前版本的说明开始，然后逐步向下操作。

* [版本 1.24.0 或更旧](from-1.x.md#updating-from-versions-older-than-1.24.1)
* [版本 1.24.1 或 1.24.2](from-1.x.md#updating-from-1.24.1-and-1.24.2)

我们仅在此提供 Docker 单机版和 Docker Swarm 环境的说明，因为 Portainer 1.x 不支持 Kubernetes 环境。

## **从 1.24.1 之前的版本更新** <a href="#updating-from-versions-older-than-1.24.1" id="updating-from-versions-older-than-1.24.1"></a>

如果您运行的版本早于 1.24.1，必须首先更新到 `portainer/portainer:1.24.2`。您的其他应用程序/容器不会被移除。

### Docker 单机版 <a href="#docker-standalone" id="docker-standalone"></a>

使用以下命令停止然后移除旧版本，然后运行 Portainer 1.24.2 版本。

```
docker stop portainer

docker rm portainer

docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer:1.24.2
```

### Docker Swarm <a href="#docker-swarm" id="docker-swarm"></a>

运行以下命令将 Portainer 服务更新到 1.24.2。这假设您的服务名为 `portainer_portainer`（您可以通过检查 `docker service ls` 的输出确认）。

```
docker service update --image portainer/portainer:1.24.2 --force portainer_portainer
```

通过登录 Portainer 并读取 UI 左下角的版本号来验证您是否正在运行 1.24.2 版本。您现在应该继续[更新到 2.0.0 版本](from-1.x.md#updating-from-1.24.1-and-1.24.2)。

## 从 1.24.1 和 1.24.2 更新 <a href="#updating-from-1.24.1-and-1.24.2" id="updating-from-1.24.1-and-1.24.2"></a>

如果您正在运行 1.24.1 或 1.24.2 版本并希望更新到最新的 Portainer 版本，必须首先更新到 `portainer/portainer-ce:2.0.0`。使用以下命令停止然后移除旧版本。您的其他应用程序/容器不会被移除。

### Docker 单机版 <a href="#docker-standalone-1" id="docker-standalone-1"></a>

```
docker stop portainer
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

### Docker Swarm <a href="#docker-swarm-1" id="docker-swarm-1"></a>

运行以下命令将 Portainer 服务更新到 2.0.0。这假设您的服务名为 `portainer_portainer`（您可以通过检查 `docker service ls` 的输出确认）。

```
docker service update --image portainer/portainer-ce:2.0.0 --force portainer_portainer
```

Portainer CE 2.0.0 现在将部署在您的系统上，使用先前版本的持久数据，并将 Portainer 数据库升级到新版本。

部署完成后，转到 `http://your-server-address:9000` 并登录。通过登录 Portainer 并读取 UI 左下角的版本号来验证您是否正在运行 2.0.0 版本。

## 从 2.0.0 更新 <a href="#updating-from-2.0.0" id="updating-from-2.0.0"></a>

更新到 2.0.0 后，您可以继续按照平台的[标准更新说明](./)操作，或者如果要迁移到商业版，可以按照[升级说明](tobe/)操作。
