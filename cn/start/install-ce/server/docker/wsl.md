# 在 WSL/Docker Desktop 上使用 Docker 安装 Portainer CE

这些安装说明适用于 Portainer 社区版(CE)。如需安装 Portainer 商业版(BE)，请参考[BE安装文档](../../../install/server/docker/wsl.md)。

## 简介

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级 Docker 容器在 Docker 引擎上运行。本文档将帮助您在 Windows WSL 和 Docker Desktop 环境上安装 Portainer Server 容器。要向现有 Portainer Server 安装添加新的 WSL/Docker Desktop 环境，请参考[Portainer Agent 安装指南](../../../../admin/environments/add/docker/agent.md)。

开始之前，您需要：

* 已安装并运行最新版本的 Docker Desktop
* 在将托管 Portainer Server 实例的机器上拥有管理员权限
* 已安装 Windows Subsystem for Linux (WSL) 并选择了 Linux 发行版。对于新安装，我们推荐 WSL2
* 默认情况下，Portainer Server 将通过端口 `9443` 暴露 UI，并通过端口 `8000` 暴露 TCP 隧道服务器。后者是可选的，仅当您计划将 Edge 计算功能与 Edge agent 一起使用时才需要

安装说明还假设您的环境满足以下条件：

* 您的环境符合[我们的系统要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能适用于其他配置，但可能需要更改配置或功能受限
* 您通过 Unix 套接字访问 Docker。或者，您也可以通过 TCP 连接
* WSL 使用的 Linux 发行版中禁用了 SELinux。如果需要 SELinux，您需要在部署 Portainer 时向 Docker 传递 `--privileged` 标志
* Docker 以 root 身份运行。无 root 的 Docker 运行 Portainer 有一些限制，并且需要额外的配置

## 部署

首先，创建 Portainer Server 用于存储其数据库的卷：

```bash
docker volume create portainer_data
```

然后，下载并安装 Portainer Server 容器：

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-standalone)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

如果出于遗留原因需要开放 HTTP 端口 `9000`，请将以下内容添加到 `docker run` 命令中：

`-p 9000:9000`

Portainer Server 现已安装完毕。您可以通过运行 `docker ps` 来检查 Portainer Server 容器是否已启动：

```bash
root@server:~# docker ps
CONTAINER ID   IMAGE                                              COMMAND                  CREATED        STATUS        PORTS                                                                                  NAMES
f4ab79732007   portainer/portainer-ce:lts                         "/portainer"             2 weeks ago    Up 29 hours   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp, 0.0.0.0:9443->9000/tcp, :::9443->9443/tcp   portainer
```

## 登录

安装完成后，您可以通过打开网页浏览器并访问以下地址来登录您的 Portainer Server 实例：

```bash
https://localhost:9443
```

如果需要，将 `localhost` 替换为相关 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

您将看到 Portainer Server 的初始设置页面。

[setup.md](../setup.md)
