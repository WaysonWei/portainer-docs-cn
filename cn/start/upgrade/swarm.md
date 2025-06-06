# 在 Docker Swarm 上更新

始终确保 Agent 版本与 Portainer Server 版本匹配。换句话说，当您安装或更新到 Portainer 2.27.6 时，请确保所有 Agent 也都在 2.27.6 版本。

从 Portainer CE 2.9 和 BE 2.10 开始，默认在端口 `9443` 上启用 HTTPS。这些说明将配置 Portainer 同时使用 `9443` 进行 HTTPS 和 `9000` 进行 HTTP 通信。您可以在更新后[完全禁用 HTTP](../../admin/settings/#force-https-only)。在使 Portainer 仅使用 HTTPS 之前，请确保所有 Agent 和 Edge Agent 都已经使用 HTTPS 与 Portainer 通信。

如果您是从 Portainer 1.x 版本更新，**必须**先[更新到 2.0.0](from-1.x.md)，**然后**再更新到最新版本，否则会遇到问题。

在开始任何更新之前，我们强烈建议[备份](../../admin/settings/general.md#back-up-portainer)当前的 Portainer 配置。

要更新 Docker Swarm 上的 Portainer Server 和 Agent，首先在 Docker Swarm 集群的管理节点上运行以下命令：

```
docker service ls 
```

记下 Portainer 的服务名称。稍后您会需要它们。

```
ID             NAME                    MODE         REPLICAS   IMAGE                          PORTS
tb9gtxc647fw   portainer-agent_agent   global       3/3        portainer/agent:2.26.0
m3a3mtuy55ed   portainer_portainer     replicated   1/1        portainer/portainer-ee:2.26.0  *:8000->8000/tcp, *:9000->9000/tcp
```

要更新 Portainer Server 到最新版本，根据您的 Portainer 版本运行以下命令之一（如果您的设置不同，请替换 `portainer_portainer` 服务名称）：

```
docker pull portainer/portainer-ee:lts
docker service update --image portainer/portainer-ee:lts --publish-add 9443:9443 --force portainer_portainer
```

```
docker pull portainer/portainer-ce:lts
docker service update --image portainer/portainer-ce:lts --publish-add 9443:9443 --force portainer_portainer
```

要更新 Portainer Agent 到最新版本，运行以下命令（如果您的设置不同，请替换 `portainer_agent` 服务名称）：

```
docker pull portainer/agent:lts
docker service update --image portainer/agent:lts --force portainer_agent 
```

这将在您的 Swarm 集群上部署最新版本的 Portainer 和 Agent，并将 Portainer 数据库升级到匹配版本。

完成后，转到 `https://your-server-address:9443` 或 `http://your-server-address:9000` 并登录。您应该注意到更新通知已消失，版本号已更新。
