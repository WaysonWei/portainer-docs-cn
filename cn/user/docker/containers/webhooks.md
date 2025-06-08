# Webhooks

Webhook是发送到您在Docker Hub或其他注册表中定义的URL的POST请求。使用webhook可以在响应事件(如仓库推送)时触发操作。

此功能仅在[Portainer商业版](https://www.portainer.io/business-upsell?from=container-webhook)中可用。

Webhook仅在非Edge环境(运行Portainer Server或Portainer Agent的环境，而非Portainer Edge Agent)上可用。这是因为到Portainer Edge Agent的隧道是按需打开的，因此无法永久暴露webhook。

## 启用容器webhook

从菜单中选择**容器**，然后选择要配置webhook的容器。

<figure><img src="../..//assets/2.15-docker_containers_container_details.gif" alt=""><figcaption></figcaption></figure>

在**容器详情**屏幕中，切换**容器webhook**选项为开启。当URL出现时，点击**复制链接**。此URL将用于在您选择的注册表中配置webhook。

<figure><img src="../..//assets/2.15-docker_containers_container_webhook.png" alt=""><figcaption></figcaption></figure>

以下示例展示如何使用`redeploy`触发webhook:

```
<form action="https://portainer:9443/api/webhooks/638e6967-ef77-4906-8af8-236800621360" method="post">
  使用相同标签的最新镜像重新部署 <input type="submit" />
</form>
```

以下示例展示如何触发webhook以更新容器使用不同的镜像标签:

```
<form action="https://portainer:9443/api/webhooks/638e6967-ef77-4906-8af8-236800621360?tag=latest" method="post">
  使用不同标签更新容器镜像 <input type="submit" />
</form>
```

## 在Docker Hub中配置webhook

要完成配置，请参考[Docker官方文档](https://docs.docker.com/docker-hub/webhooks/)。
