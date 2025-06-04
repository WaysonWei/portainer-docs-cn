# 导入现有的Kubernetes环境

通过使用[kubeconfig](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)文件，您可以在Portainer中导入现有的Kubernetes环境。Portainer将使用kubeconfig文件中的信息连接到您的环境，然后为您部署和配置Portainer Agent。

此功能仅在[Portainer商业版](https://www.portainer.io/business-upsell?from=k8s-create-from-kubeconfig)中可用。

## 要求

虽然我们已尽力支持尽可能多的配置，但为了完全支持导入过程，有一些要求：

* 您的集群必须配置并启用了负载均衡器。
* 您的kubeconfig文件必须指定`current-context`。
* 您的kubeconfig文件必须是自包含的（即仅由一个文件组成，没有外部引用）。
* 您的kubeconfig文件必须提供集群管理员级别的凭据，以便Portainer在您的集群上部署agent。

## 生成用于导入的kubeconfig文件

根据您的环境类型，可能有不同的方法来创建支持的kubeconfig文件。目前支持以下环境类型：

### 本地集群

对于本地集群，您可以使用以下kubectl命令生成支持的kubeconfig文件：

```
kubectl config view --flatten=true --minify=true > kubeconfig.yml
```

### Civo

要从Civo集群创建kubeconfig文件，请登录Civo仪表板并转到**Kubernetes**。选择要导入的集群，然后单击**Kubeconfig**标签旁边的**Click to Download**。

### Linode

要从Linode集群创建kubeconfig文件，请登录Linode仪表板，在左侧菜单中单击**Kubernetes**。选择要导入的集群，在页面右上角选择**Actions**，然后选择**Download Config**。

### DigitalOcean

要从DigitalOcean集群创建kubeconfig文件，请登录DigitalOcean仪表板，在左侧菜单中选择**Manage**，然后选择**Kubernetes**。或者，转到**Projects**，选择包含集群的项目，然后查看**Clusters**面板。选择要导入的集群，然后单击**Kubeconfig**选项下载kubeconfig文件。

### Microsoft Azure

要从Azure集群创建kubeconfig文件，请从Microsoft下载并安装[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。在Linux上启动shell会话或在Windows上启动管理员PowerShell会话，并运行以下命令：

```
az login
```

此命令第一次使用时可能需要几分钟才能完成，并且会打开浏览器窗口以验证您的Azure身份。

完成后，运行以下命令：

```
az aks get-credentials --resource-group [resource-group-name] --name [cluster-name] --file ./kubeconfig-azure.yml
```

将`[resource-group-name]`替换为包含集群的资源组名称。将`[cluster-name]`替换为您的集群名称。

## 导入您的kubeconfig文件

创建kubeconfig文件后，从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

选择**Kubernetes**选项并点击**开始向导**。然后选择**导入**选项。

导入选项仅在[Portainer商业版](https://www.portainer.io/business-upsell?from=k8s-create-from-kubeconfig)中可用。

输入集群的**名称**，然后点击**选择文件**浏览您的kubeconfig文件。

<figure><img src="../../..//assets/2.18-environments-add-k8s-import-setup.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分以进一步自定义部署。

| 字段/选项    | 概述                                                                                                                                                                                                                                                                                   |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 自定义模板 | 选择要在集群上部署的自定义模板。这对于预加载新环境与您的应用程序非常有用。除非模板指定了要使用的命名空间，否则模板将部署在默认命名空间中。您还可以设置模板所需的任何变量。 |
| 组           | 选择配置完成后要将新环境添加到的[组](../../groups.md)。                                                                                                                                                                                               |
| 标签            | 选择要添加到环境的任何[标签](../../tags.md)。                                                                                                                                                                                                                                |

<figure><img src="../../..//assets/2.19-environments-create-microk8s-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**按钮。如果您有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表，您将在其中看到配置进度。
