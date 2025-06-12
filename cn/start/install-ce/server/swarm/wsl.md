# 在WSL/Docker Desktop上使用Docker Swarm安装Portainer CE

这些安装说明适用于Portainer社区版(CE)。对于Portainer商业版(BE)，请参考[BE安装文档](../../../install/server/swarm/wsl.md)。

## 简介

Portainer由两个组件组成：_Portainer Server_和_Portainer Agent_。这两个组件都作为轻量级Docker容器运行在Docker引擎上。本文档将帮助您在Windows环境下的WSL和Docker Desktop上安装Portainer Server容器。要将新的WSL/Docker Desktop Swarm环境添加到现有的Portainer Server安装中，请参考[Portainer Agent安装说明](../../../../admin/environments/add/swarm/agent.md)。

开始之前，您需要：

* 已安装并运行最新版本的Docker Desktop
* 已[启用](https://docs.docker.com/engine/swarm/swarm-mode/)并运行Swarm模式，包括用于Swarm服务通信的overlay网络
* 对Swarm集群管理器节点具有管理员访问权限
* 已安装Windows Subsystem for Linux(WSL)并选择了Linux发行版。对于新安装，我们推荐WSL2
* 默认情况下，Portainer将通过端口`9443`暴露UI，并通过端口`8000`暴露TCP隧道服务器。后者是可选的，仅当您计划使用Edge计算功能与Edge代理时才需要
* 管理器节点和工作节点必须能够通过端口`9001`相互通信

安装说明将对您的环境做出以下假设：

* 您的环境满足[我们的要求](../../../requirements-and-prerequisites.md)。虽然Portainer可能在其他配置下工作，但可能需要配置更改或功能有限
* 您通过Unix套接字访问Docker。或者，您也可以通过TCP连接
* WSL使用的Linux发行版中禁用了SELinux
* Docker以root身份运行。无root的Docker运行Portainer有一些限制，需要额外配置
* 您在Swarm中运行单个管理器节点。如果有多个，请[阅读此知识库文章](https://portal.portainer.io/knowledge/how-can-i-ensure-portainers-configuration-is-retained)后再继续
* 如果您的节点使用DNS记录进行通信，请确保所有记录在整个集群中可解析

## 部署

Portainer可以直接作为服务部署在您的Docker Swarm集群中。请注意，此方法将自动部署Portainer Server的单个实例，并在集群中的每个节点上全局部署Portainer Agent服务。

无论您的集群中有多少节点，只需为您的环境执行此操作**一次**。您**不需要**将集群中的每个节点作为单独的环境添加到Portainer中。将清单部署到Swarm将自动包含集群中的每个节点。将每个节点添加为单独的环境也会消耗比您预期更多的许可节点数。

要开始安装，首先获取堆栈YML清单：

```bash
curl -L https://downloads.portainer.io/ce-lts/portainer-agent-stack.yml -o portainer-agent-stack.yml
```

然后使用下载的YML清单部署您的堆栈：

```bash
docker stack deploy -c portainer-agent-stack.yml portainer
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
