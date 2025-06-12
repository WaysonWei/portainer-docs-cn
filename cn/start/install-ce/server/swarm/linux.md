# 在Linux上使用Docker Swarm安装Portainer CE

这些安装说明适用于Portainer社区版(CE)。如需Portainer商业版(BE)，请参考[BE安装文档](../../../install/server/swarm/linux.md)。

## 简介 <a href="#introduction" id="introduction"></a>

Portainer由两个组件组成：_Portainer Server_和_Portainer Agent_。这两个组件都作为轻量级Docker容器运行在Docker引擎上。本文档将帮助您在Linux环境中部署Portainer Server和Agent容器。如需将新的Linux Swarm环境添加到现有的Portainer Server安装中，请参考[Portainer Agent安装说明](../../../../admin/environments/add/swarm/agent.md)。

开始之前，您需要：

* 已安装并运行最新版本的Docker。我们建议遵循Docker的[官方安装说明](https://docs.docker.com/engine/install/) - 特别建议不要在Ubuntu发行版上通过snap安装Docker，因为这可能会导致兼容性问题。
* 已[启用](https://docs.docker.com/engine/swarm/swarm-mode/)并运行Swarm模式，包括用于swarm服务通信的overlay网络
* 在swarm集群的管理节点上拥有`sudo`权限
* 默认情况下，Portainer将通过端口`9443`暴露UI界面，并通过端口`8000`暴露TCP隧道服务器。后者是可选的，仅当您计划使用Edge计算功能与Edge代理时才需要。
* 管理节点和工作节点必须能够通过端口`9001`相互通信。

安装说明还对您的环境做出以下假设：

* 您的环境满足[我们的要求](../../../requirements-and-prerequisites.md)。虽然Portainer可能在其他配置下工作，但可能需要配置更改或功能受限。
* 您通过Unix套接字访问Docker。Docker Swarm不支持通过TCP连接。
* 运行Docker的机器上已禁用SELinux。
* Docker以root身份运行。无root权限的Docker运行Portainer有一些限制，并且需要额外配置。
* 您在swarm中运行单个管理节点。如果有多个，请在进行之前[阅读此知识库文章](https://portal.portainer.io/knowledge/how-can-i-ensure-portainers-configuration-is-retained)。
* 如果您的节点使用DNS记录进行通信，请确保集群中的所有记录都可解析。

## 部署 <a href="#deployment" id="deployment"></a>
部署

Portainer可以直接作为服务部署在您的Docker集群中。请注意，此方法将自动部署单个Portainer Server实例，并在集群中的每个节点上全局部署Portainer Agent服务。

无论集群中有多少节点，只需为您的环境执行此操作**一次**。您**不需要**将集群中的每个节点作为单独的环境添加到Portainer中。将清单部署到您的swarm将自动包含集群中的每个节点。将每个节点作为单独的环境添加也会消耗比您预期更多的许可节点数。

首先，获取stack YML清单：

```
curl -L https://downloads.portainer.io/ce-lts/portainer-agent-stack.yml -o portainer-agent-stack.yml
```

然后使用下载的YML清单部署您的堆栈：

```
docker stack deploy -c portainer-agent-stack.yml portainer
```


默认情况下，Portainer会生成并使用自签名SSL证书来保护端口`9443`。或者，您可以在[安装期间](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-swarm)或安装完成后[通过Portainer UI](../../../../admin/settings/#ssl-certificate)提供自己的SSL证书。


Portainer Server和Agent现已安装完成。您可以通过运行`docker ps`来检查Portainer Server和Agent容器是否已启动：

```
root@manager01:~# docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED              STATUS              PORTS                NAMES
59ee466f6b15   portainer/agent:lts             "./agent"                About a minute ago   Up About a minute                        portainer_agent.xbb8k6r7j1tk9gozjku7e43wr.5sa6b3e8cl6hyu0snlt387sgv
2db7dd4bfba0   portainer/portainer-ce:lts      "/portainer -H tcp:/…"   About a minute ago   Up About a minute   8000/tcp, 9443/tcp   portainer_portainer.1.gpuvu3pqmt1m19zxfo44v7izx
```

## 登录 <a href="#logging-in" id="logging-in"></a>

安装完成后，您可以通过打开网页浏览器并访问以下地址登录Portainer Server实例：

```
https://localhost:9443
```

如果需要，请将`localhost`替换为相关IP地址或FQDN，如果之前更改过端口号也请相应调整。

您将看到Portainer Server的初始设置页面。


[setup.md](../setup.md)
