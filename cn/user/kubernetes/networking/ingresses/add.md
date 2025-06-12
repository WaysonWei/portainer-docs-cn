# 手动添加 Ingress

从菜单展开 **Networking**，选择 **Ingresses** 然后点击 **Add with form**。

<figure><img src="../../..//assets/2.20-kubernetes-networking-ingresses-add.gif" alt=""><figcaption></figcaption></figure>

从列表中选择需要创建 Ingress 的 **namespace**。

按照以下部分的指导完成所需信息。

### 基本配置

<table><thead><tr><th width="213">字段/选项</th><th>概述</th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td>名称</td><td>为 ingress 输入一个描述性名称。</td><td></td><td></td></tr><tr><td>Ingress 类</td><td>从列表中选择一个 Ingress Class 对象，或者当 Ingress 规范中不需要 <code>IngressClass</code> 信息时选择 <strong>none</strong>。</td><td></td><td></td></tr><tr><td>注解</td><td>您可以通过点击 <strong>Add annotation</strong> 并填写 <strong>Key</strong> 和 <strong>Value</strong> 字段来根据需要添加注解。根据您选择的 ingress 类，您还可以添加重写注解和/或正则表达式注解。</td><td></td><td></td></tr></tbody></table>

<figure><img src="../../..//assets/2.18-k8s-ingresses-add-name.png" alt=""><figcaption></figcaption></figure>


**Google Cloud 用户注意事项**

Google Cloud ingress 控制器（gce 或 GKE Ingress）继续在 ingress 上使用已弃用的 `kubernetes.io/ingress.class` 注解，而大多数其他 ingress 控制器使用 Kubernetes 1.18 中引入的 `IngressClass` 资源。

Portainer 以 `IngressClass` 资源作为指定 ingress 类的方式，但您仍然可以通过在 [Cluster setup](../../cluster/setup.md#ingress-controllers) 中打开 **Allow ingress class to be set to "none"** 开关并将其设置为自定义（选择 **Ingress class** 为 `none`）来使用 Google Cloud ingress 控制器。然后，在基于此添加 ingress 时，设置一个注解，其 **key** 为 `kubernetes.io/ingress.class`，**value** 为 `gce`。


### Ingress 规则

在此您可以定义 Ingress 规则的具体内容：

<table><thead><tr><th width="201">字段/选项</th><th>概述</th><th data-hidden></th></tr></thead><tbody><tr><td>主机名</td><td>输入应用程序应通过其访问的 FQDN<br>例如：<code>myapp.mydomain.com</code>。</td><td></td></tr><tr><td>TLS 密钥</td><td>选择包含上述主机名 SSL 证书信息的 TLS 密钥。可选地，通过点击 <strong>Create secret</strong> 链接（在新标签页打开）创建一个新的 <a href="../../configurations/add-1.md">TLS Secret</a>。密钥创建后，点击 TLS 密钥下拉菜单旁边的重新加载按钮并选择新密钥。</td><td></td></tr><tr><td>服务</td><td>从列表中选择您要暴露的服务。</td><td></td></tr><tr><td>服务端口</td><td>从列表中选择需要暴露的端口。</td><td></td></tr><tr><td>路径类型</td><td>选择相关的路径类型。默认为 <code>Prefix</code>。</td><td></td></tr><tr><td>路径</td><td>输入暴露应用程序的路径。要在域根目录上暴露，请使用 <code>/</code>。</td><td></td></tr></tbody></table>

您可以通过点击 **Add path** 使用不同路径暴露其他服务。

<figure><img src="../../..//assets/2.19-kubernetes-ingress-create-rules.png" alt=""><figcaption></figcaption></figure>

通过点击 **Add new host** 添加更多规则，或通过 **Add fallback rule** 添加回退规则。

回退规则没有指定主机名。此规则仅适用于入站请求的主机名与您的其他规则都不匹配的情况。

准备就绪后，点击 **Create**。
