# Webhooks

Webhook是一个发送到URL的POST请求。使用webhook可以在响应事件(如仓库推送)时触发操作。

此功能仅在[Portainer商业版](https://www.portainer.io/business-upsell?from=stack-webhook)中可用。

Webhook仅在非Edge环境(运行Portainer Server或Portainer Agent的环境，而非Portainer Edge Agent)中可用。这是因为到Portainer Edge Agent的隧道仅在需要时打开，因此无法永久暴露webhook。

## 启用应用webhook

从菜单选择**应用**，然后选择要配置webhook的应用。接着选择**编辑此应用**按钮。

Webhook仅适用于从Git仓库部署的应用。

<figure><img src="../..//assets/2.20-kubernetes-applications-webhooks.gif" alt=""><figcaption></figcaption></figure>

如果尚未启用，请启用**GitOps更新**并选择`Webhook`作为**机制**。当URL出现时，点击**复制链接**。这是用于触发webhook的URL。

<figure><img src="../..//assets/2.19-kubernetes-applications-webhooks-git.png" alt=""><figcaption></figcaption></figure>

以下示例展示如何触发webhook：

```
<form action="https://portainer:9443/api/stacks/webhooks/40ac1662-47c3-4a8e-b148-2a34eb52bb42" method="post">
  重新部署应用 <input type="submit" />
</form>
```

## 在webhooks中使用环境变量

触发webhook时，可以通过端点传递环境变量并在部署中引用。

环境变量不能更新Pods，只能更新Deployments。

要在webhook上指定环境变量，将其作为变量添加到URL中。例如，传递值为`development`的`SERVICE_TAG`变量：

```
https://portainer:9443/api/stacks/webhooks/40ac1662-47c3-4a8e-b148-2a34eb52bb42?SERVICE_TAG=development
```

要在manifest中引用`SERVICE_TAG`变量并回退到值`stable`：

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        env:
        - name: SERVICE_TAG 
          value: "stable"
```

环境变量必须已在manifest中定义 - 不能通过webhook添加新的环境变量。

## 滚动重启

当使用应用的webhook重新部署应用时，可以指示Portainer执行应用的滚动重启，而不是"终止并重启"的重新部署。

此功能仅在Portainer商业版中可用。

要指定此操作，在webhook调用中使用`rollout-restart`参数：

```
https://portainer:9443/api/stacks/webhooks/40ac1662-47c3-4a8e-b148-2a34eb52bb42?rollout-restart=all
```

有效选项如下：

| 选项                                                          | 概述                                                                                                                                                                                                                                                                                                                                                                    |
| --------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `rollout-restart=all`                                           | 应用的所有部署将作为滚动重启重新部署。                                                                                                                                                                                                                                                                                               |
| `rollout-restart=deployment/deployment1,deployment/deployment2` | <p>仅指定的部署将作为滚动重启重新部署。所有其他部署不会被重新部署或重启。多个部署用逗号分隔。<br>此选项支持Deployments (<code>deployment/deployment1</code>)、DaemonSets (<code>daemonset/daemonset1</code>)和StatefulSets (<code>statefulset/statefulset1</code>)。</p> |

如果未定义`rollout-restart`参数，webhook将以传统的"终止并重启"行为重新部署应用。

如果集群启用了[变更窗口](../cluster/setup.md#change-window-settings)，滚动重启将仅在变更窗口内执行。
