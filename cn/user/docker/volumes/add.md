# 添加新数据卷

## 添加本地数据卷

从菜单中选择 **Volumes**，然后点击 **Add volume**。

<figure><img src="../..//assets/2.15-docker_volumes_add_volume.gif" alt=""><figcaption></figcaption></figure>

在 **Create volume** 界面中填写信息，参考下表：

| 字段/选项       | 概述                                                                 |
| --------------- | -------------------------------------------------------------------- |
| Name            | 为数据卷指定一个描述性名称                                           |
| Driver          | 选择 `local`                                                         |
| Use NFS volume  | 关闭此选项                                                           |
| Use CIFS volume | 关闭此选项                                                           |
| Deployment      | 在多节点集群上，定义将保存数据卷的节点                               |

<figure><img src="../..//assets/2.15-docker_volumes_create_volume.png" alt=""><figcaption></figcaption></figure>

完成后，点击 **Create the volume**。

## 添加NFS数据卷

在 Portainer 中，您可以挂载 NFS 数据卷来持久化容器数据。

从菜单中选择 **Volumes**，然后点击 **Add volume**。

<figure><img src="../..//assets/2.15-docker_volumes_add_volume.gif" alt=""><figcaption></figcaption></figure>

在 **Create volume** 界面中填写信息，参考下表：

| 字段/选项       | 概述                                                                 |
| --------------- | -------------------------------------------------------------------- |
| Name            | 为数据卷指定一个描述性名称                                           |
| Driver          | 选择 `local`                                                         |
| Use NFS volume  | 开启此选项                                                           |
| Use CIFS volume | 关闭此选项                                                           |
| Deployment      | 在多节点集群上，定义将保存数据卷的节点                               |

<figure><img src="../..//assets/2.15-docker_volumes_create_volume_nfs.png" alt=""><figcaption></figcaption></figure>

在 **NFS Settings** 部分，填写以下内容：

| 字段/选项    | 概述                                                                 |
| ------------ | -------------------------------------------------------------------- |
| Address      | 输入 NFS 服务器的主机名或 IP 地址                                    |
| NFS Version  | 选择 NFS 服务器使用的 NFS 版本                                        |
| Mount point  | 输入数据卷挂载的路径，例如 `/mnt/nfs01`                              |
| Options      | 保留默认值                                                           |

<figure><img src="../..//assets/2.15-docker_volumes_create_volume_nfs_settings.png" alt=""><figcaption></figcaption></figure>

完成后，点击 **Create the volume**。

## 添加CIFS数据卷

在 Portainer 中，您可以挂载 CIFS 数据卷来持久化容器数据。

从菜单中选择 **Volumes**，然后点击 **Add volume**。

在 **Create volume** 界面中填写信息，参考下表：

| 字段/选项       | 概述                                                                 |
| --------------- | -------------------------------------------------------------------- |
| Name            | 为数据卷指定一个描述性名称                                           |
| Driver          | 选择 `local`                                                         |
| Use NFS volume  | 关闭此选项                                                           |
| Use CIFS volume | 开启此选项                                                           |
| Deployment      | 在多节点集群上，定义将保存数据卷的节点                               |

<figure><img src="../..//assets/2.15-docker_volumes_create_volume_cifs.png" alt=""><figcaption></figcaption></figure>

在 **CIFS Settings** 部分，填写以下内容：

| 字段/选项    | 概述                                                                 |
| ------------ | -------------------------------------------------------------------- |
| Address      | 输入 CIFS 服务器名称或 IP 地址                                       |
| Share        | 输入共享资源的名称                                                   |
| CIFS Version | 选择您使用的 CIFS 版本                                               |
| Username     | 输入用于身份验证的用户名                                             |
| Password     | 输入用于身份验证的密码                                               |

<figure><img src="../..//assets/2.15-docker_volumes_create_volume_cifs_settings.png" alt=""><figcaption></figcaption></figure>

完成后，点击 **Create the volume**。

## 添加tmpfs数据卷

从菜单中选择 **Volumes**，然后点击 **Add volume**。

<figure><img src="../..//assets/2.15-docker_volumes_add_volume.gif" alt=""><figcaption></figcaption></figure>

在 **Create volume** 界面中填写信息，参考下表：

| 字段/选项       | 概述                                                                 |
| --------------- | -------------------------------------------------------------------- |
| Name            | 为数据卷指定一个描述性名称                                           |
| Driver          | 选择 `local`                                                         |
| Driver options  | 点击 **add driver option** 然后添加以下名称/值组合：                 |
|                 | <ul><li><p>name: <code>type</code></p><p>value: <code>tmpfs</code></p></li><li><p>name: <code>device</code></p><p>value: <code>tmpfs</code></p></li><li>name: <code>o</code></li><li>value: <code>size=100m,uid=1000</code> (根据您的需求自定义这些值)</li></ul> |
| Use NFS volume  | 关闭此选项                                                           |
| Use CIFS volume | 关闭此选项                                                           |
| Deployment      | 在多节点集群上，定义将保存数据卷的节点                               |

<figure><img src="../..//assets/2.15-docker_volumes_create_volume_tmpfs.png" alt=""><figcaption></figcaption></figure>

完成后，点击 **Create the volume**。现在可以像其他数据卷一样将此数据卷附加到容器。

<figure><img src="../..//assets/2.15-docker_volumes_volume_adv_settings.png" alt=""><figcaption></figcaption></figure>

附加后，您可以在容器内确认 tmpfs 数据卷已正确挂载：

<figure><img src="../..//assets/2.15-docker_volumes_volume_console_exec_tmpfs.png" alt=""><figcaption></figcaption></figure>
