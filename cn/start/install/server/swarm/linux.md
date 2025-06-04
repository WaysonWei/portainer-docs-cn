# 在 Linux 上使用 Docker Swarm 安装 Portainer BE

这些安装说明适用于 Portainer 商业版(BE)。如需安装 Portainer 社区版(CE)，请参考[CE安装文档](../../../install-ce/server/swarm/linux.md)。

## 简介 <a href="#introduction" id="introduction"></a>

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级 Docker 容器运行在 Docker 引擎上。本文档将帮助您在 Linux 环境上部署 Portainer Server 和 Agent 容器。要向现有 Portainer Server 安装添加新的 Linux Swarm 环境，请参考[Portainer Agent 安装指南](../../../../admin/environments/add/swarm/agent.md)。

开始之前，您需要：

* 已安装并运行最新版本的 Docker。我们建议按照 Docker 的[官方安装说明](https://docs.docker.com/engine/install/)进行操作 - 特别建议不要通过 snap 在 Ubuntu 发行版上安装 Docker，因为可能会遇到兼容性问题
* 已[启用](https://docs.docker.com/engine/swarm/swarm-mode/)并运行 Swarm 模式，包括用于 swarm 服务通信的 overlay 网络
* 在 swarm 集群的管理节点上拥有 `sudo` 权限
* 默认情况下，Portainer 将通过端口 `9443` 暴露 UI，并通过端口 `8000` 暴露 TCP 隧道服务器。后者是可选的，仅当您计划将 Edge 计算功能与 Edge agent 一起使用时才需要
* 管理节点和工作节点必须能够通过端口 `9001` 相互通信
* Portainer 商业版的许可证密钥

安装说明还假设您的环境满足以下条件：

* 您的环境符合[我们的系统要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能适用于其他配置，但可能需要更改配置或功能受限
* 您通过 Unix 套接字访问 Docker。不支持通过 TCP 连接 Docker Swarm
* 运行 Docker 的机器上禁用了 SELinux
* Docker 以 root 身份运行。无 root 的 Docker 运行 Portainer 有一些限制，并且需要额外的配置
* 您在 swarm 中运行单个管理节点。如果有多个管理节点，请先[阅读此知识库文章](https://portal.portainer.io/knowledge/how-can-i-ensure-portainers-configuration-is-retained)
* 如果您的节点使用 DNS 记录进行通信，请确保所有记录在集群中都可解析

## 部署 <a href="#deployment" id="deployment"></a>

Portainer 可以直接作为服务部署在您的 Docker 集群中。请注意，此方法将自动部署单个 Portainer Server 实例，并在集群中的每个节点上全局部署 Portainer Agent 服务。

**无论集群中有多少节点，只需为您的环境执行此操作一次**。您**不需要**将集群中的每个节点作为单独的环境添加到 Portainer 中。将清单部署到您的 swarm 将自动包含每个节点。将每个节点添加为单独的环境也会消耗比预期更多的许可节点数。

首先，获取 stack YML 清单：

```
curl -L https://downloads.portainer.io/ee-lts/portainer-agent-stack.yml -o portainer-agent-stack.yml
```

然后使用下载的 YML 清单部署您的 stack：

```
docker stack deploy -c portainer-agent-stack.yml portainer
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-swarm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

Portainer Server 和 Agent 现已安装完毕。您可以通过运行 `docker ps` 来检查 Portainer Server 和 Agent 容器是否已启动：

```
root@manager01:~# docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED              STATUS              PORTS                NAMES
59ee466f6b15   portainer/agent:lts             "./agent"                About a minute ago   Up About a minute                        portainer_agent.xbb8k6r7j1tk9gozjku7e43wr.5sa6b3e8cl6hyu0snlt387sgv
2db7dd4bfba0   portainer/portainer-ee:lts      "/portainer -H tcp:/…"   About a minute ago   Up About a minute   8000/tcp, 9443/tcp   portainer_portainer.1.gpuvu3pqmt1m19zxfo44v7izx
```

## 登录 <a href="#logging-in" id="logging-in"></a>

安装完成后，您可以通过打开网页浏览器并访问以下地址来登录您的 Portainer Server 实例：

```
https://localhost:9443
```

如果需要，将 `localhost` 替换为相关 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

您将看到 Portainer Server 的初始设置页面。

[setup.md](../setup.md)
