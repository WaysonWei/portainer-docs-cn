# 在 Windows 容器服务上使用 Docker Swarm 安装 Portainer BE


这些安装说明适用于 Portainer 商业版(BE)。如需安装 Portainer 社区版(CE)，请参考[CE安装文档](../../../install-ce/server/swarm/wcs.md)。


## 简介

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级 Docker 容器运行在 Docker 引擎上。本文档将帮助您在 Windows 容器服务的 Windows 服务器上安装 Portainer Server 容器。要向现有 Portainer Server 安装添加新的 WCS 环境，请参考[Portainer Agent 安装指南](../../../../admin/environments/add/swarm/agent.md)。

开始之前，您需要：

* 已安装并运行最新版本的 Docker
* 已[启用](https://docs.docker.com/engine/swarm/swarm-mode/)并运行 Swarm 模式，包括用于 swarm 服务通信的 overlay 网络
* 在 Swarm 集群的管理节点上拥有管理员权限
* 默认情况下，Portainer 将通过端口 `9443` 暴露 UI，并通过端口 `8000` 暴露 TCP 隧道服务器。后者是可选的，仅当您计划将 Edge 计算功能与 Edge agent 一起使用时才需要
* 管理节点和工作节点必须能够通过端口 `9001` 相互通信
* Portainer 商业版的许可证密钥

安装说明还假设您的环境满足以下条件：

* 您的环境符合[我们的系统要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能适用于其他配置，但可能需要更改配置或功能受限
* 您在 swarm 中运行单个管理节点。如果有多个管理节点，请先[阅读此知识库文章](https://portal.portainer.io/knowledge/how-can-i-ensure-portainers-configuration-is-retained)
* 如果您的节点使用 DNS 记录进行通信，请确保所有记录在集群中都可解析

## 准备工作

要在 Windows 服务器/桌面环境中运行 Portainer Server，您需要在防火墙中创建例外。可以通过运行以下 PowerShell 命令轻松添加这些例外：

```
netsh advfirewall firewall add rule name="cluster_management" dir=in action=allow protocol=TCP localport=2377
netsh advfirewall firewall add rule name="node_communication_tcp" dir=in action=allow protocol=TCP localport=7946
netsh advfirewall firewall add rule name="node_communication_udp" dir=in action=allow protocol=UDP localport=7946
netsh advfirewall firewall add rule name="overlay_network" dir=in action=allow protocol=UDP localport=4789
netsh advfirewall firewall add rule name="swarm_dns_tcp" dir=in action=allow protocol=TCP localport=53
netsh advfirewall firewall add rule name="swarm_dns_udp" dir=in action=allow protocol=UDP localport=53
```

您还需要安装 Windows 容器主机服务和 Docker。Microsoft 已经[提供](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce#windows-server-1)了一个 PowerShell 脚本来执行必要的操作。您可以使用以下命令下载并运行该脚本：

```
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
.\install-docker-ce.ps1
```

完成此操作后，您需要重新启动 Windows 服务器。重启完成后，即可安装 Portainer。

## 部署

Portainer 可以直接作为服务部署在您的 Docker 集群中。请注意，此方法将自动部署单个 Portainer Server 实例，并在集群中的每个节点上全局部署 Portainer Agent 服务。


**无论集群中有多少节点，只需为您的环境执行此操作一次**。您**不需要**将集群中的每个节点作为单独的环境添加到 Portainer 中。将清单部署到您的 swarm 将自动包含每个节点。将每个节点添加为单独的环境也会消耗比预期更多的许可节点数。


您可以使用我们的 YML 清单在 Windows 容器中运行 Portainer。在 PowerShell 中运行：

```
curl https://downloads.portainer.io/ee-lts/portainer_windows_stack.yml -o portainer-windows-stack.yml
```

然后使用下载的 YML 清单部署您的 stack：

```bash
docker stack deploy --compose-file=portainer-windows-stack.yml portainer
```


默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-swarm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。


## 登录

安装完成后，您可以通过打开网页浏览器并访问以下地址来登录您的 Portainer Server 实例：

```bash
https://localhost:9443
```

如果需要，将 `localhost` 替换为相关 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

您将看到 Portainer Server 的初始设置页面。


[setup.md](../setup.md)
