# Ingresses

在 Kubernetes 中，**Ingress** 是一种 API 对象，提供路由规则来管理外部用户对 Kubernetes 集群中服务的访问，通常通过 HTTPS/HTTP。使用 Ingress，您可以轻松设置流量路由规则，而无需创建大量负载均衡器或在节点上暴露每个服务。

要查看、编辑或创建 Ingress，请展开左侧菜单中的 **Networking** 并选择 **Ingresses**。

<figure><img src="../../..//assets/2.20-kubernetes-networking-ingresses.gif" alt=""><figcaption></figcaption></figure>

用户有权访问的所有 Ingress 都列在此页面上。

<figure><img src="../../..//assets/2.20-kubernetes-networking-ingresses-list.png" alt=""><figcaption></figcaption></figure>

新的 Ingress 对象可以通过手动方式或通过 manifest 创建：

[add.md](add.md)

[manifest.md](manifest.md)

如果不再需要某个 Ingress，可以将其删除：

[remove-an-ingress.md](remove-an-ingress.md)
