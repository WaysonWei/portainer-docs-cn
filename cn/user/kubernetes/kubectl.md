# kubectl shell

虽然Portainer UI提供了许多Kubernetes功能，但有时您需要进入控制台。我们在UI中提供了一个包含`kubectl`和`helm`二进制文件的shell。该shell预加载了用户上下文的`kubeconfig`，限制访问Portainer中为该用户定义的权限。

要访问shell，从菜单中选择**kubectl shell**。shell加载后，您可以按需运行`kubectl`和`helm`命令。

<figure><img src="..//assets/2.20-kubernetes-kubectl.gif" alt=""><figcaption></figcaption></figure>
