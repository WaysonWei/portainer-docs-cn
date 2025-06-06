# 在 Kubernetes 上更新

始终确保 Agent 版本与 Portainer Server 版本匹配。换句话说，当您安装或更新到 Portainer 2.27.6 时，请确保所有 Agent 也都在 2.27.6 版本。

从 Portainer CE 2.9 和 BE 2.10 开始，默认在端口 `9443` 上启用 HTTPS。这些说明将配置 Portainer 同时使用 `9443` 进行 HTTPS 和 `9000` 进行 HTTP 通信。您可以在更新后[完全禁用 HTTP](../../admin/settings/#force-https-only)。在使 Portainer 仅使用 HTTPS 之前，请确保所有 Agent 和 Edge Agent 都已经使用 HTTPS 与 Portainer 通信。

在开始任何更新之前，我们强烈建议[备份](../../admin/settings/general.md#back-up-portainer)当前的 Portainer 配置。

选择与原始安装方法匹配的 Portainer 更新方法。

## 方法 1: 使用 Helm 更新

运行以下命令添加 Portainer Helm 仓库。忽略任何关于仓库已存在的警告：

```
helm repo add portainer https://portainer.github.io/k8s/
helm repo update
```

接下来，运行以下命令之一来更新 Portainer：

```
helm upgrade -n portainer portainer portainer/portainer \
    --set enterpriseEdition.image.tag=lts
```

```
helm upgrade -n portainer portainer portainer/portainer \
    --set image.tag=lts
```

## 方法 2: 使用 YAML 清单更新

### 选项 1: 通过 Portainer UI

最简单的更新方法是使用 Portainer UI 和我们的清单文件。复制与您部署 Portainer 的方法匹配的清单文件内容：

复制相关的 NodePort 清单文件内容：

**商业版：**
```
https://downloads.portainer.io/ee-lts/portainer.yaml
```

**社区版：**
```
https://downloads.portainer.io/ce-lts/portainer.yaml
```

对于仅 Agent 的部署，请改用以下清单之一：

**商业版：**
```
https://downloads.portainer.io/ee-lts/portainer-agent-k8s-nodeport.yaml
```

**社区版：**
```
https://downloads.portainer.io/ce-lts/portainer-agent-k8s-nodeport.yaml
```

如果您在 Portainer Server 实例上设置了自定义 `AGENT_SECRET`（通过在启动 Portainer Server 容器时指定 `AGENT_SECRET` 环境变量），在更新 Agent 时必须记住以相同方式（作为环境变量）显式提供相同的密钥给您的 Agent：

`environment:`
`- AGENT_SECRET: yoursecret`

复制相关的 Load Balancer 清单文件内容：

**商业版：**
```
https://downloads.portainer.io/ee-lts/portainer-lb.yaml
```

**社区版：**
```
https://downloads.portainer.io/ce-lts/portainer-lb.yaml
```

对于仅 Agent 的部署，请改用以下清单之一：

**商业版：**
```
https://downloads.portainer.io/ee-lts/portainer-agent-k8s-lb.yaml
```

**社区版：**
```
https://downloads.portainer.io/ce-lts/portainer-agent-k8s-lb.yaml
```

如果您在 Portainer Server 实例上设置了自定义 `AGENT_SECRET`，在更新 Agent 时必须记住在 YAML 中显式提供：

`environment:`
`- AGENT_SECRET: yoursecret`

登录 Portainer 并连接到安装了 Portainer 的 Kubernetes 环境。从菜单中选择 **Applications**，然后选择 **Create from manifest**。将 **Use namespace(s) specified from manifest** 切换为开启状态，然后在 **Name** 字段中输入 `portainer`。

如果您为 Portainer 部署使用了不同的名称，请改用该名称。

从 **Build method** 选择中选择 **Web Editor** 并确保 **Kubernetes** 被选为 **Deploy type**。粘贴 YAML 文件内容，然后点击 **Deploy**。Portainer 将处理清单，更新完成后应返回登录页面。

### 选项 2: 通过命令行

如果您更喜欢使用命令行更新，可以使用 `kubectl` 命令：

登录 Kubernetes 集群的控制节点并运行以下命令之一：

**商业版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer.yaml
```

**社区版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ce-lts/portainer.yaml
```

对于仅 Agent 的部署，请改用以下命令之一：

**商业版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer-agent-k8s-nodeport.yaml
```

**社区版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ce-lts/portainer-agent-k8s-nodeport.yaml
```

如果您在 Portainer Server 实例上设置了自定义 `AGENT_SECRET`（通过在启动 Portainer Server 容器时指定 `AGENT_SECRET` 环境变量），在更新 Agent 时必须记住以相同方式（作为环境变量）显式提供相同的密钥给您的 Agent：

`environment:`
`- AGENT_SECRET: yoursecret`

登录 Kubernetes 集群的控制节点并运行以下命令之一：

**商业版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer-lb.yaml
```

**社区版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ce-lts/portainer.yaml
```

对于仅 Agent 的部署，请改用以下命令之一：

**商业版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer-agent-k8s-lb.yaml
```

**社区版：**
```
kubectl apply -n portainer -f https://downloads.portainer.io/ce-lts/portainer-agent-k8s-lb.yaml
```

如果您在 Portainer Server 实例上设置了自定义 `AGENT_SECRET`，在更新 Agent 时必须记住在 YAML 中显式提供：

`environment:`
`- AGENT_SECRET: yoursecret`

部署完成后，您将能够登录 Portainer。您应该注意到 Portainer UI 左下角的新版本号。

## 方法 3: 强制更新

如果在运行上述命令后 Portainer 没有更新，您可以通过运行以下命令强制下载最新镜像：

```
kubectl -n portainer rollout restart deployment.apps/portainer
```

或者，对于仅 Agent 的部署，请改用以下命令：

```
kubectl -n portainer rollout restart deployment.apps/portainer-agent
