# Edge配置

Edge配置是可以预部署到Edge环境中的文件集合，用于为每个Edge环境提供动态可配置性，同时避免在部署仓库中存储大量配置文件。

在**Edge计算**菜单下选择**Edge配置**。

<figure><img src="..//assets/2.19-edge-configurations.gif" alt=""><figcaption></figcaption></figure>

在此您可以查看当前配置列表、它们应用的Edge组、创建和更新日期，以及将配置推送到Edge环境的进度。

<figure><img src="..//assets/2.19-edge-configurations-list.png" alt=""><figcaption></figcaption></figure>

## 添加新配置

要添加新配置，点击**添加配置**并填写表单。

| 字段/选项      | 概述                                                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------------------------------- |
| 名称            | 输入配置的名称。                                                                                                          |
| Edge组         | 选择此配置将应用的Edge组。                                                                                                |
| 目录            | 输入Edge设备上用于存储配置的目录。此目录在所有设备上应相同，并且Edge Agent运行用户应具有写入权限。                         |

<figure><img src="..//assets/2.19-edge-configurations-name.png" alt=""><figcaption></figcaption></figure>

### 类型

接下来选择要部署的配置**类型**。选择**通用配置**类型时，配置内容将部署到所选组中所有设备的指定目录，生成的配置文件将在相同位置对所有设备可用。

<figure><img src="..//assets/2.19-edge-configurations-type-general.png" alt=""><figcaption></figcaption></figure>

或者您可以选择**设备特定配置**，这将允许您根据设备的Portainer Edge ID将配置子集部署到指定设备。

您可以在**环境**下找到Edge环境的Edge ID，选择环境并注意**Edge信息**框中的**Edge标识符**值。它将如下所示：

`73149964-56f4-473b-81b3-5ecdc397e490`

您可以指定**匹配规则**，将配置中的文件名或文件夹名与Portainer Edge ID匹配。

<figure><img src="..//assets/2.19-edge-configurations-type-device-specific.png" alt=""><figcaption></figcaption></figure>

使用**文件名**匹配时，配置包中任何文件名（任何扩展名）与Edge ID匹配的文件将被部署到匹配的远程Edge环境的**目录**字段指定位置。

使用**文件夹名**匹配时，配置包中任何名称与Edge ID匹配的文件夹的内容将被部署到匹配的远程Edge环境的**目录**字段指定位置。

### 配置

最后，点击**从包上传**选择要上传的包。此包应是一个ZIP文件，包含您要部署在Edge环境上的配置文件，内容结构基于上面选择的**类型**。

使用文件夹名匹配时，您的Edge ID命名文件夹应位于包文件内容的基目录中，而不是任何子目录中。

<figure><img src="..//assets/2.19-edge-configurations-configuration.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**创建配置并推送**。您的配置将被上传到Portainer并根据您的选择部署到相关Edge环境。

## 在Edge Stack中使用Edge配置

使用Edge配置时，您的文件将在指定路径下对所选Edge设备可用。您可以直接在Edge Stack配置中引用此路径来访问其中的文件。

使用设备特定配置时，您上传的配置将根据每个设备的Portainer Edge ID具有文件名或文件夹名（取决于您的**匹配规则**选择）。您可以在堆栈文件中使用`PORTAINER_EDGE_ID`环境变量引用此ID。例如，要在每个设备上将设备特定文件夹挂载到容器中，可以使用以下语法：

```
version: '3'

services:
  myservice:
    image: myimage:latest
    volumes:
      - /var/edge/configs/${PORTAINER_EDGE_ID}:/my-device-config
```

在此示例中，堆栈部署到的每个Edge设备都会将其特定设备（基于Portainer Edge ID）文件夹挂载到容器中的`/my-device-config`文件夹。
