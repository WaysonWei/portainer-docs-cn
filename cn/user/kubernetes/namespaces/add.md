# 添加新命名空间

从菜单中选择**命名空间**，然后点击**使用表单添加**。

也可以通过点击**从manifest创建**来[使用manifest](../applications/manifest.md)添加命名空间。

<figure><img src="../..//assets/2.20-namespaces-add.gif" alt=""><figcaption></figcaption></figure>

为命名空间提供一个描述性的**名称**。作为可选步骤，您可以通过点击**添加注解**并填写**键**和**值**字段来根据需要添加注解。

<figure><img src="../..//assets/2.18-k8s-namespaces-add-name.png" alt=""><figcaption></figcaption></figure>

### 资源配额

您可以通过切换**资源分配**来分配配额，然后设置资源限制，如分配多少内存和CPU。

<figure><img src="../..//assets/2.20-kubernetes-namespaces-add-resourcequota.png" alt=""><figcaption></figcaption></figure>

### 负载均衡器

要设置可以在命名空间内创建的外部负载均衡器的最大数量，请切换**负载均衡器配额**并设置**最大负载均衡器**数量。如果启用了负载均衡器配额并将最大负载均衡器值设置为`0`，则命名空间中实际上禁用了外部负载均衡器的使用。

只有在[集群设置](../cluster/setup.md#allow-users-to-use-external-load-balancer)中启用了**允许用户使用外部负载均衡器**时，才会显示此部分。

<figure><img src="../..//assets/2.18-k8s-namespaces-add-lbquota.png" alt=""><figcaption></figcaption></figure>

### 网络 - Ingress

此部分允许您定义允许在此命名空间内用于发布应用程序的ingress控制器。勾选要允许的ingress旁边的复选框，然后点击**允许选中**，或点击**禁止选中**以禁止它们在此命名空间中的使用。

只有在[集群设置](../cluster/setup.md#networking-ingresses)中启用了**按命名空间配置Ingress控制器可用性**时，才会显示此部分。

<figure><img src="../..//assets/2.20-namespaces-add-ingress.png" alt=""><figcaption></figcaption></figure>

### 镜像仓库

您可以在此部分定义此命名空间内可用的镜像仓库。从**选择镜像仓库**下拉菜单中选择要允许访问的镜像仓库。

<figure><img src="../..//assets/2.18-k8s-namespaces-add-registries.png" alt=""><figcaption></figcaption></figure>

### 存储

使用此部分为命名空间启用存储选项的配额。要启用存储选项的配额使用，请切换**启用配额**并设置**最大使用量**。最大使用量值为`0`实际上会阻止该存储选项在命名空间中的使用。

<figure><img src="../..//assets/2.18-k8s-namespaces-add-storage.png" alt=""><figcaption></figcaption></figure>

### 摘要

此部分显示点击添加命名空间按钮时将采取的操作摘要。

<figure><img src="../..//assets/2.18-k8s-namespaces-add-summary.png" alt=""><figcaption></figcaption></figure>

完成后，点击**创建命名空间**。
