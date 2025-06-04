# 在 Linux 上使用 Podman 安装 Portainer BE

这些安装说明适用于 Portainer 商业版(BE)。如需安装 Portainer 社区版(CE)，请参考[CE安装文档](../../../install-ce/server/podman/linux.md)。

## 简介

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级容器运行在 Podman 引擎上。本文档将帮助您在 Linux 环境上安装 Portainer Server 容器。要向现有 Portainer Server 安装添加新的 Linux 环境，请参考[Portainer Agent 安装指南](../../../../admin/environments/add/podman/agent.md)。

开始之前，您需要：

* 在您的 Podman 主机上安装并运行 CentOS 9 和最新版本的 Podman 5.x。其他 Podman 版本和 Linux 发行版可能可用，但我们目前仅支持上述配置。我们建议按照 Podman 的[官方安装说明](https://podman.io/docs/installation#installing-on-linux)进行操作
* 在将托管 Portainer Server 实例的机器上拥有 sudo 权限
* 默认情况下，Portainer Server 将通过端口 `9443` 暴露 UI，并通过端口 `8000` 暴露 TCP 隧道服务器。后者是可选的，仅当您计划将 Edge 计算功能与 Edge agent 一起使用时才需要
* Portainer 商业版的许可证密钥

安装说明还假设您的环境满足以下条件：

* 您的环境符合[我们的系统要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能适用于其他配置，但可能需要更改配置或功能受限
* 您通过 Unix 套接字访问 Podman
* Podman 以 root 身份运行。无 root 的 Podman 运行 Portainer 可能可用，但目前不受官方支持

## 部署

首先，确保 Podman 套接字已启用：

```
systemctl enable --now podman.socket
```

接下来，创建 Portainer Server 用于存储其数据库的卷：

```bash
podman volume create portainer_data
```

然后，下载并安装 Portainer Server 容器：

<pre><code><strong>podman run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:lts
</strong></code></pre>

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-standalone)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

如果出于遗留原因需要开放 HTTP 端口 `9000`，请将以下内容添加到 `podman run` 命令中：

`-p 9000:9000`

Portainer Server 现已安装完毕。您可以通过运行 `podman ps` 来检查 Portainer Server 容器是否已启动：

```bash
root@server:~# podman ps
CONTAINER ID   IMAGE                          COMMAND                  CREATED       STATUS      PORTS                                                                                  NAMES             
de5b28eb2fa9   portainer/portainer-ee:lts     "/portainer"             2 weeks ago   Up 9 days   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer
```

## 登录

安装完成后，您可以通过打开网页浏览器并访问以下地址来登录您的 Portainer Server 实例：

```bash
https://localhost:9443
```

如果需要，将 `localhost` 替换为相关 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

您将看到 Portainer Server 的初始设置页面。

[setup.md](../setup.md)
