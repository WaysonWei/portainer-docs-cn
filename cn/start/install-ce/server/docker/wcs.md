# 在 Windows Container Service 上使用 Docker 安装 Portainer CE

这些安装说明适用于 Portainer 社区版(CE)。如需安装 Portainer 商业版(BE)，请参考[BE安装文档](../../../install/server/docker/wcs.md)。

## 简介

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级 Docker 容器在 Docker 引擎上运行。本文档将帮助您在 Windows Server 的 Windows 容器环境中安装 Portainer Server 容器。要向现有 Portainer Server 安装添加新的 WCS 环境，请参考[Portainer Agent 安装指南](../../../../admin/environments/add/docker/agent.md)。

开始之前，您需要：

* 在将托管 Portainer Server 实例的机器上拥有管理员权限
* 默认情况下，Portainer Server 将通过端口 `9443` 暴露 UI，并通过端口 `8000` 暴露 TCP 隧道服务器。后者是可选的，仅当您计划将 Edge 计算功能与 Edge agent 一起使用时才需要

安装说明还假设您的环境满足以下条件：

* 您的环境符合[我们的系统要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能适用于其他配置，但可能需要更改配置或功能受限

## 准备工作

要在 Windows Server/Desktop 环境中运行 Portainer Server，您需要在防火墙中添加例外规则。可以通过 PowerShell 运行以下命令轻松添加：

```
netsh advfirewall firewall add rule name="cluster_management" dir=in action=allow protocol=TCP localport=2377
netsh advfirewall firewall add rule name="node_communication_tcp" dir=in action=allow protocol=TCP localport=7946
netsh advfirewall firewall add rule name="node_communication_udp" dir=in action=allow protocol=UDP localport=7946
netsh advfirewall firewall add rule name="overlay_network" dir=in action=allow protocol=UDP localport=4789
netsh advfirewall firewall add rule name="swarm_dns_tcp" dir=in action=allow protocol=TCP localport=53
netsh advfirewall firewall add rule name="swarm_dns_udp" dir=in action=allow protocol=UDP localport=53
```

您还需要安装 Windows 容器主机服务并安装 Docker。Microsoft 提供了 [PowerShell 脚本](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce#windows-server-1)来执行必要的操作。您可以使用以下命令下载并运行该脚本：

```
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
.\install-docker-ce.ps1
```

完成后，您需要重启 Windows 服务器。重启完成后，即可安装 Portainer。

## 部署

首先，创建 Portainer Server 用于存储其数据库的卷。使用 PowerShell：

```
docker volume create portainer_data
```

然后，下载并安装 Portainer Server 容器：

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart always -v \\.\pipe\docker_engine:\\.\pipe\docker_engine -v portainer_data:C:\data portainer/portainer-ce:lts
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

如果看到类似以下的错误消息：

`"\\.\pipe\dockerDesktopEngine" includes invalid characters for a local volume name`

则可能没有正确启用 Windows 容器。如果使用 Docker Desktop，请右键单击系统托盘中的图标并选择 **Switch to Windows Containers**。

如果出于遗留原因需要开放 HTTP 端口 `9000`，请将以下内容添加到 `docker run` 命令中：

`-p 9000:9000`

## 登录

安装完成后，您可以通过打开网页浏览器并访问以下地址来登录您的 Portainer Server 实例：

```bash
https://localhost:9443
```

如果需要，将 `localhost` 替换为相关 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

您将看到 Portainer Server 的初始设置页面。

[setup.md](../setup.md)
