# 管理命名空间

从菜单中选择**命名空间**，然后选择要管理的命名空间。

<figure><img src="../..//assets/2.20-namespaces-manage.gif" alt=""><figcaption></figcaption></figure>

在这里您可以查看命名空间的详细信息并配置特定于该命名空间的选项。

## 资源配额

切换**资源分配**为此命名空间启用配额，然后定义内存和CPU限制。设置限制后，将显示命名空间的当前资源预留和使用情况。

<figure><img src="../..//assets/2.25-kubernetes-namespaces-manage-resourcequota.png" alt=""><figcaption></figcaption></figure>

## 负载均衡器

通过此设置，您可以配置在此命名空间中可以创建的外部负载均衡器数量。

只有在[集群设置](../cluster/setup.md#allow-users-to-use-external-load-balancer)中启用了**允许用户使用外部负载均衡器**时，才会显示此选项。

<figure><img src="../..//assets/2.17-k8s-namespaces-manage-loadbalancer.png" alt=""><figcaption></figcaption></figure>

## 网络

此部分允许您定义哪些ingress控制器可以用于在此命名空间内发布应用程序。勾选要允许的ingress旁边的复选框，然后点击**允许选中**，或点击**禁止选中**以禁止它们在此命名空间中的使用。

只有在[集群设置](../cluster/setup.md#networking-ingresses)中启用了**按命名空间配置Ingress控制器可用性**时，才会显示此部分。

<figure><img src="../..//assets/2.20-namespaces-add-ingress.png" alt=""><figcaption></figcaption></figure>

## 镜像仓库

在此部分，您可以定义此命名空间内可用的镜像仓库。从**选择镜像仓库**下拉菜单中选择要允许访问的镜像仓库。

<figure><img src="../..//assets/2.18-k8s-namespaces-add-registries.png" alt=""><figcaption></figcaption></figure>

## 存储

对于集群中可用的每个存储选项，您可以为此命名空间配置配额以限制使用。

<figure><img src="../..//assets/2.15-kubernetes_namespaces_manage_namespace_storage.png" alt=""><figcaption></figcaption></figure>

## 摘要

如果您对配置进行了更改，此部分将列出这些更改。

<figure><img src="../..//assets/2.15-kubernetes_namespaces_manage_namespaces_summary.png" alt=""><figcaption></figcaption></figure>

## 操作

完成必要的更改后，点击**更新命名空间**。您还可以通过点击**标记为系统**将命名空间标记为系统命名空间。

<figure><img src="../..//assets/2.15-kubernetes_namespaces_manage_namespaces_actions.png" alt=""><figcaption></figcaption></figure>
