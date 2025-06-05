# Kubeconfig

Portainer可以作为其他Kubernetes管理工具的代理，提供对Kubernetes集群的访问，同时保留Portainer提供的安全性和治理功能。用户可以下载自己的`kubeconfig`文件，并使用他们喜欢的工具来访问Kubernetes集群，仅具有该用户被授予的权限。

要生成并下载您的`kubeconfig`文件，从首页点击**kubeconfig**按钮。

您必须通过HTTPS访问Portainer才能看到kubeconfig按钮。如果您使用HTTP登录，将看不到此选项。

<figure><img src="..//assets/2.15-k8s-kubeconfig.gif" alt=""><figcaption></figcaption></figure>

系统会要求您选择要包含在`kubeconfig`文件中的Kubernetes环境。如果您配置了[kubeconfig过期时间](../../admin/settings/#kubeconfig-expiry)值，也会显示在此处。

<figure><img src="..//assets/2.15-k8s-kubeconfig-confirm.png" alt=""><figcaption></figcaption></figure>

勾选所需环境的复选框，然后点击**下载文件**。

下载的`kubeconfig`文件将类似于以下示例。

请注意，服务器URL设置为Portainer Server实例，而不是Kubernetes集群。

```yaml
apiVersion: v1
clusters:
- cluster:
    insecure-skip-tls-verify: true
    server: https://my-portainer-server:9443/api/endpoints/1/kubernetes
  name: portainer-cluster-kubernetes
contexts:
- context:
    cluster: portainer-cluster-kubernetes
    user: portainer-sa-clusteradmin
  name: portainer-ctx-kubernetes
current-context: portainer-ctx-kubernetes
kind: Config
preferences: {}
users:
- name: portainer-sa-clusteradmin
  user:
    token: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

`kubeconfig`中的每个环境都可以通过上下文访问。访问权限基于创建`kubeconfig`文件的特定用户设置。

除非设置为永不过期，否则令牌将在定义的时间段后过期，此时需要生成新的`kubeconfig`文件。管理员可以在**设置**页面[调整令牌过期行为](../../admin/settings/#kubeconfig-expiry)。

调整令牌过期时间不会影响先前生成的`kubeconfig`文件。
