# 设置

您可以通过从菜单展开**集群**然后选择**设置**来更改环境的Kubernetes配置。

<figure><img src="../..//assets/2.20-kubernetes-cluster-setup.gif" alt=""><figcaption></figcaption></figure>

## 网络 - 服务

### 允许用户使用外部负载均衡器

要使用此功能，您需要确保您的云提供商允许您创建负载均衡器。使用此功能可能会产生云提供商的费用。

启用负载均衡器功能将允许用户通过其云提供商分配的外部IP地址公开他们部署的应用程序。

<figure><img src="../..//assets/2.20-kubernetes-cluster-setup-networking-services.png" alt=""><figcaption></figcaption></figure>

## 网络 - Ingress

配置Ingress控制器将允许用户通过HTTP路由公开他们部署的应用程序。

Portainer自动检测并列出集群中定义的任何Ingress控制器，并默认设置为允许。作为管理员，您可以根据需要禁用Ingress控制器。

<figure><img src="../..//assets/2.19-kubernetes-cluster-setup-ingresses.png" alt=""><figcaption></figcaption></figure>

启用**允许将Ingress类设置为"none"**将允许用户创建不指定任何Ingress类的Ingress对象。这对于集群中没有定义`IngressClass`的Kubernetes实现很有用。

启用**按命名空间配置Ingress控制器可用性**切换，可以进一步在命名空间级别控制Ingress类的可用性。

启用**仅允许管理员部署Ingress**将限制只有集群管理员才能部署Ingress，防止标准用户创建新的Ingress。

## 变更窗口设置

此设置允许您指定一个窗口，在此窗口内可以应用对应用程序的[GitOps更新](../applications/manifest.md#gitops-updates)。

如果启用此设置并在窗口之外对应用程序进行更新，则不会应用该更新。

<figure><img src="../..//assets/2.20-kubernetes-cluster-setup-changewindow.png" alt=""><figcaption></figcaption></figure>

## 部署选项

此部分允许您覆盖为Kubernetes环境设置的任何全局部署选项。

此部分仅在[设置](../../../admin/settings/#deployment-options)中启用了**允许按环境覆盖**选项时出现。

| 字段/选项                             | 概述                                                                                                                                                                       |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 覆盖全局部署选项       | 启用此选项以覆盖此环境的全局部署选项。                                                                                             |
| 强制基于代码的部署            | 当覆盖启用时，启用此选项将在部署应用程序时隐藏"使用表单添加"按钮，并防止通过表单添加或编辑Kubernetes资源。 |
| 允许使用Web编辑器和自定义模板 | 当强制基于代码的部署时，启用此选项以允许在部署应用程序时使用Web编辑器和自定义模板。                                     |
| 允许通过URL指定清单 | 当强制基于代码的部署时，启用此选项以允许在部署应用程序时使用URL选项。                                                             |

<figure><img src="../..//assets/2.20-kubernetes-cluster-setup-deployment.png" alt=""><figcaption></figcaption></figure>

## 安全

### 限制对默认命名空间的访问

默认情况下，Kubernetes集群在配置集群时会实例化一个默认命名空间，以保存集群使用的默认Pod、服务和部署集。如果启用此选项，唯一有权在默认命名空间中运行应用程序的用户是Portainer管理员。

### 限制非管理员用户访问secret内容(仅限UI)

默认情况下，用户能够在Portainer UI中查看和编辑Kubernetes secret。启用此选项将禁止所有非管理员用户这样做。请注意，由于Kubernetes本身的限制，这仅适用于Portainer UI，并不阻止用户通过命令行或API这样做。

<figure><img src="../..//assets/2.20-kubernetes-cluster-setup-security.png" alt=""><figcaption></figcaption></figure>

## 资源和指标

### 允许资源超额分配

启用此功能可让您为命名空间分配比集群中物理可用资源更多的资源。

**启用**资源超额分配，如果您需要为命名空间分配比集群中物理可用资源更多的资源。如果资源不足以满足需求，这可能会导致意外的部署失败。

**禁用**资源超额分配(强烈推荐)，如果您只能为命名空间分配的资源总量小于集群总量减去任何系统资源预留。

### 使用指标API启用功能

确保Kubernetes[指标服务器](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-metrics-pipeline/#metrics-server)或[Prometheus](https://github.com/kubernetes-sigs/prometheus-adapter)在您的集群中运行。

启用此功能将允许用户使用利用指标API组件的特定功能，例如集群和节点级别的内存和CPU使用情况图表。如果Portainer检测到您正在使用指标服务器并且能够连接，则此选项将默认为开启。

<figure><img src="../..//assets/2.15-k8s-cluster-setup-resources.png" alt=""><figcaption></figcaption></figure>

## 可用存储选项

选择部署应用程序时可用的存储选项。查看您的存储驱动程序文档以确定要配置的访问策略，以及是否支持卷扩展功能。标记为默认的任何存储类将自动设置为开启。

<figure><img src="../..//assets/2.15-k8s-cluster-setup-storage.png" alt=""><figcaption></figcaption></figure>
