# 添加ConfigMap

从菜单选择**ConfigMaps & Secrets**，确保选中**ConfigMaps**标签页，然后点击**使用表单添加**。

ConfigMaps也可以通过[使用manifest](../applications/manifest.md)添加，点击**从manifest创建**。

<figure><img src="../..//assets/2.19-kubernetes-configurations-configmaps-add.gif" alt=""><figcaption></figcaption></figure>

定义ConfigMap，参考下方表格作为指南。

| 字段/选项      | 概述                                                                                                                               |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| 命名空间    | 选择ConfigMap将保存的命名空间。                                                                                |
| 名称         | 为ConfigMap指定一个描述性名称。                                                                                                 |
| 注解  | 可以按需点击**添加注解**并填写**键**和**值**字段来为ConfigMap添加注解。  |

<figure><img src="../..//assets/2.19-kubernetes-configurations-configmaps-add.png" alt=""><figcaption></figcaption></figure>

在**数据**部分，您可以在**简单模式**或**高级模式**下输入ConfigMap的详细信息。在简单模式下可以以键值对格式添加条目，在高级模式下可以粘贴YAML格式的多个值。

<figure><img src="../..//assets/2.15-kubernetes_configmap_add_form_config_data.png" alt=""><figcaption><p>在简单模式下添加数据</p></figcaption></figure>

<figure><img src="../..//assets/2.15-kubernetes_configmap_add_from_config_data_simple.png" alt=""><figcaption><p>在高级模式下添加数据</p></figcaption></figure>

完成ConfigMap定义后，点击**创建ConfigMap**。
