# 在Windows容器服务上使用Docker Swarm安装Portainer CE

这些安装说明适用于Portainer社区版(CE)。对于Portainer商业版(BE)，请参考[BE安装文档](../../../install/server/swarm/wcs.md)。

## 简介

Portainer由两个组件组成：_Portainer Server_和_Portainer Agent_。这两个组件都作为轻量级Docker容器运行在Docker引擎上。本文档将帮助您在Windows容器服务上安装Portainer Server容器。要将新的WCS环境添加到现有的Portainer Server安装中，请参考[Portainer Agent安装说明](../../../../admin/environments/add/swarm/agent.md)。

开始前，您需要：

* 已安装并运行最新版本的Docker
* 已[启用](https://docs.docker.com/engine/swarm/swarm-mode/)并运行Swarm模式，包括用于Swarm服务通信的overlay网络
* 对Swarm集群管理节点具有管理员访问权限
* 默认情况下，Portainer将通过端口`9443`暴露UI，并通过端口`8000`暴露TCP隧道服务器。后者是可选的，仅在您计划使用Edge计算功能与Edge代理时才需要
* 管理节点和工作节点必须能够通过端口`9001`相互通信

安装说明还假设您的环境满足以下条件：

* 您的环境满足[我们的要求](../../../requirements-and-prerequisites.md)。虽然Portainer可能在其他配置下工作，但可能需要更改配置或功能受限
* 您在Swarm中运行单个管理节点。如果有多个，请继续之前[阅读此知识库文章](https://portal.portainer.io/knowledge/how-can-i-ensure-portainers-configuration-is-retained)
* 如果您的节点使用DNS记录进行通信，请确保所有记录在整个集群中可解析

## 准备工作

要在Windows Server/Desktop环境中运行Portainer Server，您需要在防火墙中添加例外。可以通过PowerShell运行以下命令轻松添加：

```
netsh advfirewall firewall add rule name="cluster_management" dir=in action=allow protocol=TCP localport=2377
netsh advfirewall firewall add rule name="node_communication_tcp" dir=in action=allow protocol=TCP localport=7946
netsh advfirewall firewall add rule name="node_communication_udp" dir=in action=allow protocol=UDP localport=7946
netsh advfirewall firewall add rule name="overlay_network" dir=in action=allow protocol=UDP localport=4789
netsh advfirewall firewall add rule name="swarm_dns_tcp" dir=in action=allow protocol=TCP localport=53
netsh advfirewall firewall add rule name="swarm_dns_udp" dir=in action=allow protocol=UDP localport=53
```

您还需要安装Windows容器主机服务并安装Docker。Microsoft提供了[PowerShell脚本](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce#windows-server-1)来执行必要的操作。您可以使用以下命令下载并运行该脚本：

```
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
.\install-docker-ce.ps1
```

完成后需要重启Windows服务器。重启完成后即可安装Portainer。

## 部署

Portainer可以直接作为服务部署在Docker集群中。此方法会自动部署单个Portainer Server实例，并在集群每个节点上全局部署Portainer Agent服务。


无论集群中有多少节点，只需为您的环境执行此操作**一次**。您**不需要**将集群中的每个节点作为单独的环境添加到Portainer中。将清单部署到swarm会自动包含集群中的每个节点。将每个节点作为单独的环境添加也会消耗比预期更多的许可节点数。


您可以使用我们的YML清单在Windows容器中运行Portainer。在PowerShell中运行：

```
curl https://downloads.portainer.io/ce-lts/portainer_windows_stack.yml -o portainer-windows-stack.yml
```

然后使用下载的YML清单部署您的堆栈：

```bash
docker stack deploy --compose-file=portainer-windows-stack.yml portainer
```


默认情况下，Portainer会生成并使用自签名SSL证书来保护端口`9443`。或者，您可以在[安装期间](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-swarm)或安装完成后[通过Portainer UI](../../../../admin/settings/#ssl-certificate)提供自己的SSL证书。


## 登录

安装完成后，您可以通过打开网页浏览器并访问以下地址登录Portainer Server实例：

```bash
https://localhost:9443
```

如果需要，请将`localhost`替换为相关IP地址或FQDN，如果之前更改过端口号也请相应调整。

您将看到Portainer Server的初始设置页面。


[setup.md](../setup.md)
