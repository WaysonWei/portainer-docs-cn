# 更改容器所有权

Portainer允许您将容器管理权限限制给特定团队或用户。

从菜单中选择**容器**，然后选择要更改所有权的容器。

<figure><img src="../..//assets/2.15-docker_containers_container_details.gif" alt=""><figcaption></figcaption></figure>

在**访问控制**部分勾选**更改所有权**复选框，然后选择新的所有权类型，参考下表作为指南：

| 所有权类型     | 概述                                                                                                    |
| -------------- | ----------------------------------------------------------------------------------------------------------- |
| 管理员        | 只有Portainer管理员可以管理该容器。                                                     |
| 受限          | 只有您指定的团队或用户可以管理该容器。                                                   |
| 公开          | 任何拥有[环境访问权限](../../../admin/environments/access.md)的人都可以管理该容器。 |

<figure><img src="../..//assets/2.15-docker_containers_container_access_control.png" alt=""><figcaption></figcaption></figure>

选择完成后，点击**更新所有权**。当确认消息出现时，点击**更改所有权**。

<figure><img src="../..//assets/2.15-container-ownership-confirm.png" alt=""><figcaption></figcaption></figure>
