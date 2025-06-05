# 在 Kubernetes 环境安装 Portainer BE

这些安装说明适用于 Portainer 商业版(BE)。如需安装 Portainer 社区版(CE)，请参考[CE安装文档](../../../install-ce/server/kubernetes/baremetal.md)。

## 简介

Portainer 由两个组件组成：_Portainer Server_ 和 _Portainer Agent_。这两个组件都作为轻量级容器在 Kubernetes 上运行。

开始之前，您需要：

* 一个正常工作的最新 Kubernetes 集群
* 能够在集群上运行 `helm` 或 `kubectl` 命令的权限
* Kubernetes 集群上的 Cluster Admin 权限，以便 Portainer 可以创建必要的 `ServiceAccount` 和 `ClusterRoleBinding` 来访问集群
* 配置了 `default` StorageClass（见下文）
* Portainer 商业版的许可证密钥

安装说明还假设您的环境满足以下条件：

* 您的环境符合[我们的系统要求](../../../requirements-and-prerequisites.md)。虽然 Portainer 可能适用于其他配置，但可能需要更改配置或功能受限
* Kubernetes RBAC 已启用并正常工作（这是 Portainer 中访问控制功能所必需的）
* 您将使用 `portainer` 命名空间来安装 Portainer。目前这是一个要求 - 其他命名空间目前不受支持
* Kubernetes 的 metrics server 已安装并正常工作（如果您希望在 Portainer 中使用指标）

## 数据持久化

Portainer 需要数据持久化，因此至少需要一个可用的 StorageClass。Portainer 将在部署期间尝试使用默认的 StorageClass。如果您没有标记为 `default` 的 StorageClass，部署可能会失败。

我们建议为 Kubernetes 使用块存储而不是网络存储，以获得最佳性能和可靠性，但在选择要使用的卷时请注意块存储设备的 IOPS，因为某些选项比其他选项慢。

您可以通过在集群上运行以下命令来检查是否有默认的 StorageClass：

```
kubectl get sc
```

并查找名称后带有 `(default)` 的 StorageClass：

```
root@kubemaster01:~# kubectl get sc
NAME                            PROVISIONER                                   RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
managed-nfs-storage (default)   k8s-sigs.io/nfs-subdir-external-provisioner   Delete          Immediate           false                  11d
```

要将 StorageClass 设置为默认，可以使用以下命令：

```
kubectl patch storageclass <storage-class-name> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

将 `<storage-class-name>` 替换为您的 StorageClass 名称。或者，如果您使用我们的 Helm chart 安装，可以在 helm install 命令中传递以下参数来指定 Portainer 使用的 StorageClass：

```
--set persistence.storageClass=<storage-class-name>
```

在某些 Kubernetes 集群（例如 microk8s）中，默认的 StorageClass 只是创建 hostPath 卷，这些卷没有明确绑定到特定节点。在多节点集群中，当 pod 终止并在不同节点上重新调度时，这可能会产生问题，"留下"所有持久数据并启动带有"空"卷的 pod。

虽然这种行为本质上是使用 hostPath 卷的限制，但一个合适的解决方法是在部署中添加 nodeSelector，这实际上将 Portainer pod"固定"到特定节点。您可以通过编辑自己的 values.yaml 文件来设置 nodeSelector 值：

`nodeSelector: kubernetes.io/hostname: \<YOUR_NODE_NAME>`

或者按照下面每种部署方法的说明进行操作。

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

使用以下命令，Portainer 将在端口 `30779` 上提供 HTTPS 访问：

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set enterpriseEdition.enabled=true \
    --set enterpriseEdition.image.tag=lts \
    --set tls.force=true
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `30779`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

如果您需要通过 HTTP 在端口 `30777` 上访问 Portainer，请移除 `--set tls.force=true` 选项。

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

如果您需要通过 HTTP 访问 Portainer，请移除 `--set tls.force=true` 选项。

使用以下命令，Portainer 将在分配的 Load Balancer IP 上的端口 `9443` 上提供 HTTPS 访问：

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set service.type=LoadBalancer \
    --set enterpriseEdition.enabled=true \
    --set enterpriseEdition.image.tag=lts \
    --set tls.force=true
```

默认情况下，Portainer 生成并使用自签名 SSL 证书来保护端口 `9443`。或者，您可以在安装期间[提供自己的 SSL 证书](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm)，或在安装完成后[通过 Portainer UI](../../../../admin/settings/#ssl-certificate) 提供。

如果您需要通过 HTTP 在端口 `9000` 上访问 Portainer，请移除 `--set tls.force=true` 选项。

如果您想在 CLI 上部署 Helm chart 时明确设置目标节点，请在 `helm install` 命令中包含 `--set nodeSelector.kubernetes\.io/hostname=<YOUR NODE NAME>`。

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

如果您想在使用 YAML manifests 部署时明确设置目标节点，请运行以下一行命令来"修补"部署，强制 pod 始终调度到当前运行的节点上：

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
