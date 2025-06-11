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

You will also need to install the Windows Container Host Service and install Docker. Microsoft have [provided](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce#windows-server-1) a PowerShell script to perform the necessary actions. You can download the script and run it with the following commands:

```
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
.\install-docker-ce.ps1
```

Once this is complete you will need to restart your Windows server. After the restart completes, you're ready to install Portainer itself.

## Deployment

Portainer can be directly deployed as a service in your Docker cluster. Note that this method will automatically deploy a single instance of the Portainer Server, and deploy the Portainer Agent as a global service on every node in your cluster.


Only do this **once** for your environment, regardless of how many nodes are in the cluster. You **do not** need to add each node in your cluster as a separate environment in Portainer. Deploying the manifest to your swarm will include every node in the cluster automatically. Adding each node as a separate environment will also consume more of your licensed node count than you may expect.


You can use our YML manifest to run Portainer in Windows using Windows Containers. In PowerShell, run:

```
curl https://downloads.portainer.io/ce-lts/portainer_windows_stack.yml -o portainer-windows-stack.yml
```

Then use the downloaded YML manifest to deploy your stack:

```bash
docker stack deploy --compose-file=portainer-windows-stack.yml portainer
```


By default, Portainer generates and uses a self-signed SSL certificate to secure port `9443`. Alternatively you can provide your own SSL certificate [during installation](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-swarm) or [via the Portainer UI](../../../../admin/settings/#ssl-certificate) after installation is complete.


## Logging In

Now that the installation is complete, you can log into your Portainer Server instance by opening a web browser and going to:

```bash
https://localhost:9443
```

Replace `localhost` with the relevant IP address or FQDN if needed, and adjust the port if you changed it earlier.

You will be presented with the initial setup page for Portainer Server.


[setup.md](../setup.md)

