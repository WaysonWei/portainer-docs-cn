# Kubernetes

选择与原始安装方法匹配的 Portainer CE 到 Portainer 商业版升级方法。

## 方法 1: 通过 Helm 升级

首先运行以下命令更新 Helm 仓库：

```
helm repo update
```

接下来运行此命令，使用 Helm 部署中的所有设置，在您的 Kubernetes 集群上部署最新版本的 Portainer 商业版：

```
helm upgrade -n portainer portainer portainer/portainer --set enterpriseEdition.enabled=true
```

## 方法 2: 通过 YAML 清单升级

根据您的原始部署选择正确的 YAML 清单：

使用以下 `kubectl` 命令更新 NodePort 部署：

```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer.yaml
```

使用以下 `kubectl` 命令更新 Load Balancer 部署：

```
kubectl apply -n portainer -f https://downloads.portainer.io/ee-lts/portainer-lb.yaml
```

这将在您的 Kubernetes 集群上部署最新版本的 Portainer 商业版。

## 重新登录

升级完成后，退出 Portainer（如果当前已登录）然后重新登录。当您首次登录时，系统会要求您输入许可证密钥。从我们发送的电子邮件中粘贴此密钥。

<figure><img src="../..//assets/2.20-initial-setup-license.png" alt=""><figcaption></figcaption></figure>

左下角现在会显示"Business Edition"。
