# 在 Linux 上使用 Podman 安装 Portainer CE


这些安装说明适用于 Portainer Community Edition (CE)。对于 Portainer Business Edition (BE)，请参考 [BE 安装文档](../../../install/server/podman/linux.md)。


## 介绍

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级容器运行在 Podman 引擎上。本文档将帮助您在 Linux 环境中安装 Portainer Server 容器。要将新的 Linux 环境添加到现有的 Portainer Server 安装中，请参考 [Portainer Agent 安装说明](../../../../admin/environments/add/podman/agent.md)。

开始之前，您需要：

* CentOS 9 并在您的 Podman 主机上安装并运行最新版本的 Podman 5.x。其他 Podman 版本和 Linux 发行版可能也能工作，但我们目前仅支持上述配置。我们建议遵循 Podman 的 [官方安装说明](https://podman.io/docs/installation#installing-on-linux)。
* 在将托管 Portainer Server 实例的机器上具有 sudo 访问权限
* 默认情况下，Portainer Server 将在端口 `9443` 上公开 UI，并在端口 `8000` 上公开 TCP 隧道服务器。后者是可选的，仅在您计划将 Edge 计算功能与 Edge agent 一起使用时才需要。

安装说明还对您的环境做出以下假设：

* 您的环境满足 [我们的要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能在其他配置下工作，但可能需要配置更改或功能受限。
* 您通过 Unix sockets 访问 Podman。
* Podman 以 root 身份运行。Portainer 与 rootless Podman 可能可以工作，但目前不是官方支持的配置。

## 部署

首先，确保启用 Podman socket：

```
systemctl enable --now podman.socket
```

接下来，创建 Portainer Server 将用于存储其数据库的卷：

```bash
podman volume create portainer_data
```

然后，下载并安装 Portainer Server 容器：

<pre><code><strong>podman run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
</strong></code></pre>


默认情况下，Portainer 会生成并使用自签名的 SSL 证书来保护端口 `9443`。您也可以在 [安装过程中](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-standalone) 或安装完成后 [通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供自己的 SSL 证书。



如果由于遗留原因需要开放 HTTP 端口 `9000`，请在 `podman run` 命令中添加以下参数：

`-p 9000:9000`


Portainer Server 现已安装完成。您可以通过运行 `podman ps` 来检查 Portainer Server 容器是否已启动：

```bash
root@server:~# podman ps
CONTAINER ID   IMAGE                          COMMAND                  CREATED       STATUS      PORTS                                                                                  NAMES             
de5b28eb2fa9   portainer/portainer-ce:lts     "/portainer"             2 weeks ago   Up 9 days   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer
```

## 登录

安装完成后，您可以通过打开网页浏览器并访问以下地址来登录您的 Portainer Server 实例：

```bash
https://localhost:9443
```

如果需要，请将 `localhost` 替换为相关的 IP 地址或 FQDN，如果您之前更改了端口号，也请相应调整。

您将看到 Portainer Server 的初始设置页面。


[setup.md](../../../install-ce/server/setup.md)
