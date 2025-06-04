# 在Podman上安装Portainer Agent

Portainer使用_Portainer Agent_容器与_Portainer Server_实例通信并提供对节点资源的访问。本文档将介绍如何在节点上安装Portainer Agent以及如何从Portainer Server实例连接到它。如果您还没有可用的Portainer Server实例，请先参考[Portainer Server安装指南](../../../../start/install/server/docker/linux.md)。

除了Podman环境的通用要求外，您还需要：

* 此机器上的端口`9001`可从Portainer Server实例访问。如果不可用，我们建议改用[Edge Agent](../docker/edge.md)。

Portainer Agent安装说明还对您的环境做出以下额外假设：

* 您通过Unix sockets访问Podman。Portainer Agent不支持通过TCP连接到Podman引擎。
* 您没有在Portainer Server实例上设置自定义`AGENT_SECRET`。如果设置了（通过在启动Portainer Server容器时指定`AGENT_SECRET`环境变量），部署时需要以相同方式（作为环境变量）向您的agent提供相同的密钥，例如在`podman run`命令中添加：

    `-e AGENT_SECRET=yoursecret`

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

接下来，选择**Podman**作为环境类型，然后点击**开始向导**。选择**Agent**选项，然后选择您的环境类型。复制命令并在您的Podman实例上运行它们。

如果要使用Portainer Agent的[主机管理功能](../../../../user/docker/host/setup.md#enable-host-management-features)，您应该向Portainer提供的命令添加必要的卷挂载：

```
-v /:/host
```

如果您部署Agent的环境中的Podman卷路径位于非标准位置（而不是`/var/lib/containers/storage/volumes`），您需要调整部署命令中的卷挂载以适应。

例如，如果您的卷路径是`/srv/data/podman`，您需要将命令中的行更改为：

```
- v /srv/data/podman:/var/lib/docker/volumes \
```

挂载的右侧应保持为`/var/lib/docker/volumes`，因为这是Agent期望的（即使在使用Podman时）。

部署Agent后，请参考下表输入环境详细信息：

| 字段/选项        | 概述                                                                                                             |
| ------------------- | -------------------------------------------------------------------------------------------------------------------- |
| 名称                | 为环境指定一个描述性名称。                                                                             |
| 环境地址 | 输入连接Portainer Agent的DNS名称或IP地址以及端口（默认端口为`9001`）。 |

<figure><img src="../../..//assets/2.22.0-environments-add-podman-agent.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分，通过将环境添加到[组](../../groups.md)或添加[标签](../../tags.md)来分类环境，以便更好地搜索。

<figure><img src="../../..//assets/2.18-environments-add-docker-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您还有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
