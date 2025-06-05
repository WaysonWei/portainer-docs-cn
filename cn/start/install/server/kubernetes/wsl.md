# 在 WSL/Docker Desktop 上使用 Kubernetes 安装 Portainer BE

这些安装说明适用于 Portainer 商业版(BE)。如需安装 Portainer 社区版(CE)，请参考[CE安装文档](../../../install-ce/server/kubernetes/wsl.md)。

## 简介

以下说明将指导您在运行于 Docker Desktop 和 WSL 上的 Kubernetes 中设置 _Portainer Server_。

此方案仅用于测试目的。

我们已知在通过 Docker Desktop 运行 Kubernetes 时，命名空间和应用程序访问权限未完全实现的问题。我们正在调查根本原因，希望尽快解决。

## 准备工作

开始之前，您必须确保 Kubernetes 已在 Docker Desktop 安装中启用并运行。要在 Docker Desktop 中启用 Kubernetes，需要打开 Docker Desktop 仪表板。右键单击系统托盘中的 Docker 图标并点击**仪表板**：

![](../../..//assets/kube-wsl-1.png)

点击**设置**，然后选择**Kubernetes**，勾选**启用 Kubernetes**，然后点击**应用并重启**（在对话框中点击**安装**以安装 Kubernetes）：

![](../../..//assets/kube-wsl-2.gif)

几分钟后，您将在 Docker Desktop 左下角状态栏看到 Kubernetes 正在运行：

![左侧是 Docker，右侧是 Kubernetes](../../..//assets/kube-wsl-4.png)

## 部署

要在 Kubernetes 集群中部署 Portainer，您可以使用我们提供的 Helm charts 或 YAML manifests。

### 使用 Helm 部署

确保您至少使用 Helm v3.2，它支持 `--create-namespace` 参数。

首先通过运行以下命令添加 Portainer Helm 仓库：

```
helm repo add portainer https://portainer.github.io/k8s/
helm repo update
```

更新完成后，您就可以开始安装了。您选择的方法取决于您希望如何暴露 Portainer 服务：

使用以下命令，Portainer 将在端口 `30777` 上提供 HTTP 访问，在端口 `30779` 上提供 HTTPS 访问：

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set enterpriseEdition.enabled=true \
    --set enterpriseEdition.image.tag=lts
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

在此示例中，Portainer 将部署到您的集群并分配一个 Cluster IP，并在定义的主机名处使用 nginx Ingress Controller。有关 Ingress 选项的更多信息，请参阅[Chart 配置选项](../../../../advanced/helm-chart-configuration-options.md)列表。

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set enterpriseEdition.enabled=true \
    --set enterpriseEdition.image.tag=lts \
    --set service.type=ClusterIP \
    --set tls.force=true \
    --set ingress.enabled=true \
    --set ingress.ingressClassName=<ingressClassName (eg: nginx)> \
    --set ingress.annotations."nginx\.ingress\.kubernetes\.io/backend-protocol"=HTTPS \
    --set ingress.hosts[0].host=<fqdn (eg: portainer.example.io)> \
    --set ingress.hosts[0].paths[0].path="/"
```

使用以下命令，Portainer 将在分配的 Load Balancer IP 上的端口 `9000` 上提供 HTTP 访问，在端口 `9443` 上提供 HTTPS 访问：

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set service.type=LoadBalancer \
    --set enterpriseEdition.enabled=true \
    --set enterpriseEdition.image.tag=lts
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

要在 CLI 上部署 Helm chart 时明确设置目标节点，请在 `helm install` 命令中包含 `--set nodeSelector.kubernetes.io/hostname=<YOUR NODE NAME>`。

### 使用 YAML manifests 部署

我们的 YAML manifests 支持通过 NodePort 或 Load Balancer 暴露 Portainer。

要通过 NodePort 暴露，可以使用以下命令（Portainer 将在端口 `30777` 上提供 HTTP 访问，在端口 `30779` 上提供 HTTPS 访问）：

```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer.yaml
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `30779`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

要通过 Load Balancer 暴露，使用以下命令在分配的 Load Balancer IP 上的端口 `9000` 上提供 HTTP 访问，在端口 `9443` 上提供 HTTPS 访问：

```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer-lb.yaml
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

要在使用 YAML manifests 部署时明确设置目标节点，请运行以下一行命令来"修补"部署，强制 pod 始终调度到当前运行的节点上：

```
kubectl patch deployments -n portainer portainer -p '{"spec": {"template": {"spec": {"nodeSelector": {"kubernetes.io/hostname": "'$(kubectl get pods -n portainer -o jsonpath='{ ..nodeName }')'"}}}}}' || (echo Failed to identify current node of portainer pod; exit 1)
```

## 登录

安装完成后，您可以登录到您的 Portainer Server 实例。根据您选择暴露 Portainer 安装的方式，打开网页浏览器并导航到以下 URL：

```bash
https://localhost:30779/ or http://localhost:30777/
```

如果需要，将 `localhost` 替换为相关 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

```bash
https://<FQDN>/
```

将 `<FQDN>` 替换为您的 Portainer 实例的 FQDN。

```bash
https://<loadbalancer IP>:9443/ or http://<loadbalancer IP>:9000/
```

将 `<loadbalancer IP>` 替换为负载均衡器的 IP 地址或 FQDN，如果之前更改过端口，也请相应调整。

您将看到 Portainer Server 的初始设置页面。

[setup.md](../setup.md)
