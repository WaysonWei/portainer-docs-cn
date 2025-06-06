# 更新 Edge Agent

要将 Portainer Edge Agent 更新到最新版本，请按照以下适用于您 Edge 环境的说明操作。

始终确保 Agent 版本与 Portainer Server 版本匹配。换句话说，当您安装或更新到 Portainer 2.27.6 时，请确保所有 Agent 也都在 2.27.6 版本。

在开始任何更新之前，我们强烈建议[备份](../../admin/settings/general.md#back-up-portainer)当前的 Portainer 配置。

## Docker 单机版

Portainer 现在能够[直接从 UI 内部](../../admin/environments/update.md)更新 Docker 单机版上的 Edge Agent。

要升级 Docker 单机平台上的 Portainer Edge Agent，首先需要记下 Edge 环境的 **Edge 标识符** 和 **Edge 密钥**。要查找这些值，请登录 Portainer 并点击 **环境**，然后点击您要更新的环境名称。

在页面顶部的 **Edge 信息** 部分，您将看到下一步需要的两个值。

<figure><img src="..//assets/2.15-upgrade-edge-edgeinfo.png" alt=""><figcaption></figcaption></figure>

接下来，在 Edge 环境上，我们需要停止并移除 Edge Agent 容器。

```
docker stop portainer_edge_agent
docker rm portainer_edge_agent
```

我们还需要确保本地有更新后的容器镜像：

```
docker pull portainer/agent:lts
```

要部署更新后的 Edge Agent，请将以下命令中的 `your-edge-identifier-here` 和 `your-edge-key-here` 替换为您之前获取的值，然后运行命令：

```
docker run -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/volumes:/var/lib/docker/volumes -v /:/host -v portainer_agent_data:/data --restart always -e EDGE=1 -e EDGE_ID=your-edge-identifier-here -e EDGE_KEY=your-edge-key-here -e EDGE_INSECURE_POLL=1 --name portainer_edge_agent portainer/agent:lts
```

## Docker Swarm

要更新 Docker Swarm 环境上的 Portainer Edge Agent，请运行以下命令。

首先，确保本地有更新后的容器镜像：

```
docker pull portainer/agent:lts
```

然后，更新服务以使用新镜像版本：

```
docker service update --image portainer/agent:lts --force portainer_edge_agent 
```

## Kubernetes

要更新 Kubernetes 环境上的 Portainer Edge Agent，您需要先下载更新后的 YAML 清单，然后将其应用到现有环境。

要下载清单，可以使用以下命令之一：

```
curl -L https://downloads.portainer.io/ee-lts/portainer-agent-edge-k8s.yaml  -o portainer-agent-edge-k8s.yaml
```

```
curl -L https://downloads.portainer.io/ce-lts/portainer-agent-edge-k8s.yaml -o portainer-agent-edge-k8s.yaml  
```

要将此清单应用到您的环境，请运行以下命令：

```
kubectl apply -f portainer-agent-edge-k8s.yaml
