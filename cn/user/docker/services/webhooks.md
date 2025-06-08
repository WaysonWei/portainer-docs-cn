# Webhooks

Webhook是发送到您在Docker Hub或其他注册表中定义的URL的POST请求。使用webhook可以在响应仓库推送事件时触发操作或服务。

Webhook仅在非Edge环境(运行Portainer Server或Portainer Agent的环境，而非Portainer Edge Agent)上可用。这是因为到Portainer Edge Agent的隧道是按需打开的，因此无法永久暴露webhook。

## 启用服务webhook

从菜单选择**服务**，然后选择要配置webhook的服务。

<figure><img src="../..//assets/2.15-docker_services.gif" alt=""><figcaption></figcaption></figure>

在**服务详情**屏幕中，切换**服务webhook**选项为开启。当URL出现时，点击**复制链接**。此URL将用于在您选择的注册表中配置webhook。

<figure><img src="../..//assets/2.15-docker_services_service_webhook.png" alt=""><figcaption></figcaption></figure>

此示例展示如何使用`redeploy`触发webhook:

```
<form action="https://portainer:9443/api/webhooks/638e6967-ef77-4906-8af8-236800621360" method="post">
  使用相同标签的最新镜像重新部署 <input type="submit" />
</form>
```

此示例展示如何使用`update service image with a different tag`触发webhook:

```
<form action="https://portainer:9443/api/webhooks/638e6967-ef77-4906-8af8-236800621360?tag=latest" method="post">
  使用不同标签更新服务镜像 <input type="submit" />
</form>
```

## 在webhook中使用环境变量

触发webhook时，可以通过端点传递环境变量并在服务的compose文件中引用。

此功能仅在Portainer商业版中可用。

要在webhook上指定环境变量，将其作为变量添加到URL中。例如，传递值为`development`的`SERVICE_TAG`变量:

```
https://portainer:9443/api/webhooks/1d251d96-fb34-4172-a0a1-d0655467b897?SERVICE_TAG=development
```

要在compose文件中引用`SERVICE_TAG`变量并回退到值`stable`:

```
services:
  my-service:
    image: repository/image:${SERVICE_TAG:-stable}
```

## 在Docker Hub中配置webhook

要完成配置，请参考[Docker官方文档](https://docs.docker.com/docker-hub/webhooks/)。
