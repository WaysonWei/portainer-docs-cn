# Edge组

Edge组功能允许您通过手动选择或基于[标签](../../admin/environments/tags.md)将Edge环境分组。这在管理多个区域中的多个Edge环境时非常有用。

此功能需要您[启用边缘计算](../../admin/settings/edge.md)功能。

从菜单中选择**Edge组**，然后点击**添加Edge组**。

<figure><img src="..//assets/2.15-edge-groups.gif" alt=""><figcaption></figcaption></figure>

为组指定一个描述性名称，然后选择**静态**或**动态**：

<figure><img src="..//assets/2.15-edge-groups-name.png" alt=""><figcaption></figcaption></figure>

### **选项1: 静态**

此选项允许您从列表中手动添加环境到组中。选择所需环境，然后点击**添加Edge组**。

<figure><img src="..//assets/2.15-edge-groups-static.png" alt=""><figcaption></figcaption></figure>

### 选项2: 动态

此选项允许您通过标签自动关联环境。如果选择此选项，您需要细化Edge环境的动态关联方式。

| 选项        | 概述                                                                                                              |
| ------------- | --------------------------------------------------------------------------------------------------------------------- |
| 部分匹配 | 将关联至少匹配一个所选标签的任何环境（环境可以有多个标签）。 |
| 完全匹配    | 将关联匹配所有所选标签的任何环境。                                                    |

当您从下拉菜单中选择一个标签时，具有该标签的环境将出现在结果中。

<figure><img src="..//assets/2.15-edge-groups-dynamic.png" alt=""><figcaption></figcaption></figure>

点击**添加Edge组**将环境关联到组中。
