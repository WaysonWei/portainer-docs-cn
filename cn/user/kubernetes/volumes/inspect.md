# 检查卷

从菜单中选择**Volumes**，然后选择要检查的卷。

<figure><img src="../..//assets/2.15-k8s_kubernetes_volume_inspect.gif" alt=""><figcaption></figcaption></figure>

选择卷后，屏幕将分为三个部分，每个部分描述如下。

## 卷部分

总结有关卷的关键信息。

| 属性               | 概述                                                                                                                                             |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Name               | 卷的名称。                                                                                                                                      |
| Namespace          | 卷所属的命名空间。                                                                                                                              |
| Storage            | 卷使用的存储对象。                                                                                                                              |
| Shared Access Policy | 为卷配置的访问策略。                                                                                                                            |
| Provisioner        | 提供卷的存储供应器。                                                                                                                            |
| Creation date      | 卷的创建时间。                                                                                                                                  |
| Size               | 卷的大小。可以通过点击**Increase size**按钮并调整值来增加卷的大小。不支持缩小卷。                                                                |

<figure><img src="../..//assets/2.15-kubernetes_volumes_volume_section.png" alt=""><figcaption></figcaption></figure>

## 事件部分

显示与卷相关的事件信息。

<figure><img src="../..//assets/2.15-k8s-volumes-inspect-events.png" alt=""><figcaption></figcaption></figure>

## YAML部分

显示从卷部署生成的YAML。可用于创建配置备份。

<figure><img src="../..//assets/2.15-kubernetes_volume_volume_yaml.png" alt=""><figcaption></figcaption></figure>
