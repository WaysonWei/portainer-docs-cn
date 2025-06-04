# 在Kubernetes环境上安装Portainer Agent

Portainer由两个组件组成：_Portainer Server_和_Portainer Agent_。这两个组件都作为轻量级容器运行在Kubernetes上。本文档将介绍如何在集群上安装Portainer Agent以及如何从Portainer Server实例连接到它。如果您还没有可用的Portainer Server实例，请先参考[Portainer Server安装指南](../../../../start/install/server/kubernetes/baremetal.md)。

除了Kubernetes环境的通用要求外，您还需要：

* 能够在集群上运行`kubectl`命令的权限。
* Kubernetes集群上的Cluster Admin权限。这是为了让Portainer能够创建必要的`ServiceAccount`和`ClusterRoleBinding`来访问Kubernetes集群。

安装说明还对您的环境做出以下额外假设：

* 如果您设置了`AGENT_SECRET`环境变量（在启动Portainer Server容器时指定），您需要通过相同的方式（作为环境变量）将该密钥提供给agent，方法是将其添加到agent部署定义的YAML文件中：

    `env:`

    &#x20; `- name: AGENT_SECRET`

    &#x20;   `value: yoursecret`

要在Kubernetes集群中部署Portainer Agent，您可以使用我们提供的YAML清单。

仅agent部署的Helm图表将很快提供。

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

选择**Kubernetes**选项并点击**开始向导**。选择**Agent**选项并选择与您的配置匹配的标签页（**通过负载均衡器的Kubernetes**或**通过节点端口的Kubernetes**）。复制命令，然后在Kubernetes集群的控制节点上运行它。

在继续之前，请确保在Kubernetes节点上运行此命令。

<figure><img src="../../..//assets/2.18-environments-add-k8s-agent-command.png" alt=""><figcaption></figcaption></figure>

部署命令将返回类似以下内容：

```
namespace/portainer created
serviceaccount/portainer-sa-clusteradmin created
clusterrolebinding.rbac.authorization.k8s.io/portainer-crb-clusteradmin created
service/portainer-agent created
service/portainer-agent-headless created
deployment.apps/portainer-agent created
```

要验证agent是否正在运行，请使用以下命令：

```
 kubectl get pods --namespace=portainer
```

结果应如下所示：

```
NAME                               READY   STATUS    RESTARTS   AGE
portainer-agent-5988b5d966-bvm9m   1/1     Running   0          15m
```

无论使用哪种方法，一旦agent在Kubernetes主机上运行，您必须填写适当的环境详细信息。

无论集群中有多少个节点，只需为您的环境执行此操作**一次**。您**不需要**将每个节点作为单独的环境添加到Portainer中。只需添加一个节点即可让Portainer管理整个集群。

| 字段/选项        | 概述                                                                                                                                                                                |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 名称                | 为环境指定一个描述性名称。                                                                                                                                                |
| 环境地址 | 定义用于连接到环境的IP地址或名称（Kubernetes主机），并在需要时指定端口（使用NodePort时为`30778`；使用Load Balancer时为`9001`）。 |

<figure><img src="../../..//assets/2.15-k8s_env_url.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分以进一步自定义部署。

| 字段/选项    | 概述                                                                                                                                                                                                                                                                                   |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 自定义模板 | 选择要在集群上部署的自定义模板。这对于预加载新环境与您的应用程序非常有用。除非模板指定了要使用的命名空间，否则模板将部署在默认命名空间中。您还可以设置模板所需的任何变量。 |
| 组           | 选择配置完成后要将新环境添加到的[组](../../groups.md)。                                                                                                                                                                                               |
| 标签            | 选择要添加到环境的任何[标签](../../tags.md)。                                                                                                                                                                                                                                |

<figure><img src="../../..//assets/2.19-environments-create-microk8s-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
