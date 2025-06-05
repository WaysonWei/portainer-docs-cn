# 使用表单添加新应用

有两种方式添加新应用：手动使用表单，或自动[使用代码](manifest.md)。本文介绍如何使用表单添加应用。

<figure><img src="../..//assets/2.24.0-kubernetes-applications-form-add.gif" alt=""><figcaption></figcaption></figure>

填写所需信息，参考以下部分作为指南。

### 基础配置

| 字段/选项      | 概述                                                                                                                                                                                                      |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 命名空间    | 选择应用所在的命名空间。                                                                                                                                                                                       |
| 名称         | 为应用指定一个描述性名称。                                                                                                                                                                      |
| 注册表     | 选择拉取镜像的注册表。如果想从Portainer未配置的注册表拉取，点击**高级模式**然后手动输入URL和镜像。                         |
| 镜像        | 输入用于部署应用的镜像名称（可选包含标签）。                                                                                                             |
| 备注         | 输入备注以提供关于应用的额外详情。如果[设置](../../../admin/settings/#deployment-options)中启用了"应用需要备注"开关，此字段为必填项。 |
| 注解  | 可以按需点击**添加注解**并填写**键**和**值**字段来为应用添加注解。                                                                       |
| 堆栈        | Portainer可以自动将多个应用打包到一个堆栈中。可以输入新堆栈名称，从列表选择现有堆栈，或留空使用应用名称。    |

<figure><img src="../..//assets/2.20-kubernetes-applications-add-base.png" alt=""><figcaption></figcaption></figure>

### 环境变量

在此可以定义希望应用可用的任何环境变量。

<figure><img src="../..//assets/2.18-k8s-applications-add-envvar.png" alt=""><figcaption></figcaption></figure>

### ConfigMaps

选择之前创建的任何ConfigMap使其对应用可用。Portainer会自动将ConfigMap的所有键作为环境变量暴露。可以通过**覆盖**按钮将此行为覆盖为文件系统挂载。

<figure><img src="../..//assets/2.19-kubernetes-applications-add-form-configmaps.png" alt=""><figcaption></figcaption></figure>

### Secrets

选择之前创建的任何secret使其对应用可用。Portainer会自动将secret的所有键作为环境变量暴露。可以通过**覆盖**按钮将此行为覆盖为文件系统挂载。

<figure><img src="../..//assets/2.19-kubernetes-applications-add-form-secrets.png" alt=""><figcaption></figcaption></figure>

### 持久化文件夹

定义应用内的任何持久化文件夹，以及这些是新卷还是现有卷，以及卷大小和存储位置。

还可以为持久化文件夹定义**数据访问策略**：

* **隔离：** 每个应用实例使用自己的数据。
* **共享**：所有应用实例使用相同数据。

<figure><img src="../..//assets/2.18-k8s-applications-add-persisted.png" alt=""><figcaption></figcaption></figure>

### 资源预留

在此部分可以定义应用可用的**内存**和**CPU**量。如果所选命名空间设置了资源配额，则必须定义这些值。

<figure><img src="../..//assets/2.20-kubernetes-applications-add-resource.png" alt=""><figcaption></figcaption></figure>

### 部署

此部分允许选择如何在集群内部署应用。选项有：

* **复制：** 运行此容器的一个或多个实例。
* **全局：** 在每个集群节点上部署此容器的一个实例。

还可以通过设置**实例数**来定义要运行的应用实例数量。

<figure><img src="../..//assets/2.15-kubernetes_applications_add_form_deployment.png" alt=""><figcaption></figcaption></figure>

切换**为此应用启用自动扩展**以启用自动扩展。这需要Kubernetes指标服务器已安装并在[集群设置](../cluster/setup.md#resources-and-metrics)中启用。

| 字段/选项      | 概述                                                                                                                                                                                |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 最小实例数 | 输入希望为此应用运行的最小实例数。                                                                                                       |
| 最大实例数 | 输入希望为此应用运行的最大实例数。                                                                                                       |
| 目标CPU使用率  | 输入应用的目标CPU百分比。自动扩展器将确保运行足够的实例以在所有实例中维持此值的平均CPU使用率。 |

<figure><img src="../..//assets/2.20-kubernetes-applications-add-autoscaling.png" alt=""><figcaption></figcaption></figure>

### 放置偏好和约束

在此可以定义应用部署到的节点必须遵循的放置规则。放置规则基于节点标签。要创建新规则，点击**添加规则**。

还可以为设置的规则定义放置策略。选项有：

* **强制：** 应用仅会调度到遵循所有规则的节点上。
* **首选**：如果可能，应用将调度到遵循所有规则的节点上。

<figure><img src="../..//assets/2.20-kubernetes-applications-add-placementprefs.png" alt=""><figcaption></figcaption></figure>

### 发布应用

在此可以创建必要的服务来暴露应用。从标签页选择服务类型（ClusterIP、NodePort或LoadBalancer）并点击**创建服务**。然后可以按需配置每个服务，包括如果需要为服务添加注解。

可以展开**说明**链接获取每种服务类型工作原理的更多详情。

<figure><img src="../..//assets/2.19-kubernetes-applications-add-publishing.png" alt=""><figcaption></figcaption></figure>

完成后，点击**部署应用**。
