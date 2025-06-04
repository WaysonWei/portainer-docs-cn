# Talos Kubernetes

## 介绍

Portainer由两个组件组成：_Portainer Server_和_Portainer Agent_。这两个组件都作为轻量级容器运行在Kubernetes上。本文档将介绍如何通过Omni创建Talos Kubernetes集群并安装Portainer Edge Agent。如果您还没有可用的Portainer Server实例，请先参考[Portainer Server安装指南](../../../../start/install/server/kubernetes/baremetal.md)。

## 前提条件

为了连接到Omni并部署Talos Kubernetes集群和Portainer Edge Agent，您需要：

* 已安装Omni。您可以使用[SaaS选项](https://www.siderolabs.com/platform/saas-for-kubernetes/)或[自托管](https://omni.siderolabs.com/how-to-guides/self_hosted)Omni安装。请注意，虽然我们相信自托管安装可以正常工作，但我们尚未在此功能的初始版本中对其进行广泛测试。
* 在您的Omni安装上为Portainer使用的服务账户。此服务账户应具有管理员访问权限。您可以在我们的[凭据文档](../../../settings/credentials/omni.md)中了解如何创建服务账户。
* 在您的Omni安装中注册的机器用于您的Talos集群。有关注册这些机器的文档可以在[Sidero的文档](https://omni.siderolabs.com/how-to-guides/registering-machines)中找到。
* 您打算用于Talos Kubernetes集群的机器必须能够与Portainer Server部署在API端口（默认为`9443`）和隧道服务器端口（默认为`8000`）上进行通信。这样部署在集群上的Edge Agent可以与Portainer服务器通信。

## 部署

要创建您的Talos Kubernetes集群并将Portainer Edge Agent部署到您的机器上，从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

选择**创建Kubernetes集群**并点击**开始向导**，然后确保选择了**Talos Kubernetes**。

如果您尚未[为您的Omni安装配置一组凭据](../../../settings/credentials/omni.md)，系统将要求您现在提供它们。如果您已经配置了凭据集，可以跳转到[集群配置](omni.md#configure-your-cluster)。

### 凭据详情

根据下表填写字段：

| 字段/选项        | 概述                                                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| 凭据名称    | 输入此凭据集的名称。这将决定它在Portainer中的显示方式。                                              |
| 端点URL        | 输入您的Omni安装的端点URL。这通常是您用于访问Omni web UI的相同URL。 |
| 服务账户密钥 | 将您的服务账户密钥粘贴到此字段中。                                                                                |


您可以通过Omni web UI或使用`omnictl`创建服务账户。您可以在我们的[Omni凭据文档](../../../settings/credentials/omni.md)中找到有关如何执行此操作的更多信息。


<figure><img src="../../..//assets/2.26-environments-add-kube-create-omni-creds.png" alt=""><figcaption></figcaption></figure>

输入凭据后，点击**添加凭据**。凭据集将以您输入的名称保存，您将被带到集群配置页面。

### 配置您的集群

配置好凭据集后，您可以继续配置集群。为集群输入一个**名称**，并根据下表填写其余字段。

#### Portainer服务器详情

在这里，您可以提供Portainer的详细信息，以便在集群创建后部署代理。请注意，这里的URL应该是从集群中的机器角度可访问的Portainer URL。

| 字段/选项                    | 概述                                                                                                   |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Portainer API服务器URL        | 您的Portainer服务器的URL。这通常应预先填充正确的值。           |
| Portainer隧道服务器地址 | Portainer隧道服务器的地址。这通常应预先填充正确的值。 |

<figure><img src="../../..//assets/2.26-environments-add-kube-create-omni-portainer.png" alt=""><figcaption></figcaption></figure>

#### Omni集群摘要

在这里，您可以选择用于连接到Omni的凭据以及要部署的Talos和Kubernetes版本。

| 字段/选项       | 概述                                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| 凭据        | 从下拉列表中选择要使用的Omni凭据集。                                                                                         |
| Talos版本      | 选择要在集群机器上部署的Talos版本。此处的选项可能会受到您稍后在此过程中选择的机器的限制。     |
| Kubernetes版本 | 选择要在集群机器上安装的Kubernetes版本。此处的选项可能会根据上面选择的Talos版本受到限制。 |

<figure><img src="../../..//assets/2.26-environments-add-kube-create-omni-clustersummary.png" alt=""><figcaption></figcaption></figure>

#### 集群机器

在这里，您可以指定用于集群的机器。下拉菜单将显示可用机器列表以及每台机器上的任何标签以帮助识别。&#x20;

| 字段/选项     | 概述                                                                                                                                                 |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 控制平面    | 选择要用作控制平面节点的机器。您需要至少选择一个，建议选择奇数个控制平面节点。 |
| 主工作池 | 选择要用作工作节点的机器。                                                                                                       |

<figure><img src="../../..//assets/2.26-environments-add-kube-create-omni-machines (1).png" alt=""><figcaption></figcaption></figure>

在此处选择机器后，如果需要，您可以通过单击机器旁边的齿轮图标单独调整每台机器的网络配置。

<figure><img src="../../..//assets/2.26-environments-add-kube-create-omni-machines-customconfig-form.png" alt=""><figcaption></figcaption></figure>

以这种方式调整过网络配置的机器将在齿轮图标上有一个橙色圆点：

<figure><img src="../../..//assets/2.26-environments-add-kube-create-omni-machines-customconfig.png" alt=""><figcaption><p>talos-w1e-4a0具有修改后的网络配置，而talos-y3d-vuj没有。</p></figcaption></figure>
