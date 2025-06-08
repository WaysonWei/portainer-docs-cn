# 从已部署堆栈创建模板

在Portainer中，您可以从已部署的堆栈创建[应用模板](../templates/)。这在需要多次部署相同堆栈时非常有用。

从菜单选择**堆栈**，选择已部署的堆栈，然后点击**从堆栈创建模板**。

<figure><img src="../..//assets/2.20-stacks-template.gif" alt=""><figcaption></figcaption></figure>

为新模板定义一些属性，参考下方表格作为指南。

| 字段/选项       | 概述                                                                                    |
| --------------- | --------------------------------------------------------------------------------------- |
| 标题            | 为模板提供一个描述性名称。                                                              |
| 描述            | 输入模板包含内容的简要描述。                                                            |
| 备注            | 记录有关模板的任何额外信息(可选)。                                                      |
| Logo           | 输入模板在列表中显示时使用的Logo URL(可选)。                                            |
| 平台            | 选择模板兼容的平台。选项为**Linux**或**Windows**。                                      |
| 类型            | 选择模板类型。选项为**Standalone / Podman**或**Swarm**。                                |

<figure><img src="../..//assets/2.22.0-templates-custom-new.png" alt=""><figcaption></figcaption></figure>

**Web编辑器**将预填充堆栈的Compose文件。您可以在此处进行任何需要的更改。

随时可以按`Ctrl-F`(Mac上是`Cmd-F`)在Web编辑器中搜索。

<figure><img src="../..//assets/2.20-stacks-template-webeditor.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**创建自定义模板**。
