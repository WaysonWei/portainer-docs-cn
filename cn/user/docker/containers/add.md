# 添加新容器

从菜单中选择**容器**，然后点击**添加容器**。

<figure><img src="../..//assets/2.15-docker_containers_add_container.gif" alt=""><figcaption></figcaption></figure>

根据需要配置容器设置。

## 镜像配置部分

| 字段/选项          | 概述                                                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| 名称                  | 为容器指定一个描述性名称。                                                                                                     |
| 镜像仓库              | 选择包含您要用于容器的镜像的仓库。                                                       |
| 镜像                 | 输入您要使用的镜像名称。                                                                                               |
| 始终拉取镜像 | 切换开启以强制从仓库拉取镜像而不是使用本地缓存的副本（如果您之前使用过该镜像）。 |

<figure><img src="../..//assets/2.15-docker_containers_image_config.png" alt=""><figcaption></figcaption></figure>

使用Docker Hub时，您可以使用**搜索**按钮搜索您输入的镜像，并确保您有正确的名称和标签。使用匿名账户时，Portainer还会显示您的Docker Hub账户剩余的拉取次数。

或者，您可以切换到高级模式手动输入仓库和镜像详细信息。如果您想从Portainer中未配置的仓库进行一次性容器部署，这很有用。

<figure><img src="../..//assets/2.15-docker_containers_image_config_simple.png" alt=""><figcaption></figcaption></figure>

## Webhooks

切换**创建容器webhook**开启以为容器创建[webhook](webhooks.md)。您可以向此端点发送POST请求以自动拉取最新镜像并重新部署容器。

<figure><img src="../..//assets/2.15-docker_container_webhook.png" alt=""><figcaption></figcaption></figure>

## 网络端口配置部分

| 字段/选项                                           | 概述                                                                                                 |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| 将所有暴露的网络端口发布到随机主机端口 | 切换开启以允许Portainer将主机上的端口随机分配给容器中暴露的端口。 |
| 手动网络端口发布                         | 点击**发布新网络端口**为容器创建手动端口映射。                   |

<figure><img src="../..//assets/2.15-docker_container_network_port_config.png" alt=""><figcaption></figcaption></figure>

## 操作部分

| 字段/选项 | 概述                                                                                                                            |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| 自动移除  | 切换此选项开启以在容器退出后自动移除它。如果您只想运行容器一次，这很有用。 |

<figure><img src="../..//assets/2.15-docker_container_actions.png" alt=""><figcaption></figcaption></figure>

完成后，设置任何高级选项（见下文），然后点击**部署容器**。如果成功，您的容器将显示在容器列表中。

## 高级容器设置

从[一系列选项](advanced.md)中选择以自定义部署。

<figure><img src="../..//assets/2.15-containers-advanced.png" alt=""><figcaption></figcaption></figure>
