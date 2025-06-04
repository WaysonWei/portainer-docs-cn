# 自动加入

此部分允许您创建自定义脚本来自动快速加入多个Edge Agent。您的选择将更新页面底部提供的脚本，然后您可以在远程环境上运行该脚本。

首先，选择Edge Agent部署类型：**Edge Agent标准版**或**Edge Agent异步版**。

Portainer Edge Agent可以以两种不同模式部署 - **标准模式**和**异步模式**。在标准模式下，我们提供通过从Edge Agent到Portainer Server按需建立的隧道连接远程Edge Agent的能力，让您可以实时直接与环境交互。

在异步模式下，此隧道连接不可用。相反，我们提供浏览远程环境快照的能力，允许您基于Edge Agent环境最近发送到Portainer Server的状态捕获查看其状态，并使用此快照对远程环境执行操作。

异步模式专为使用极少数据量而开发，因此适用于连接有限或间歇性连接以及数据上限有限的连接环境，例如移动网络。

如果需要直接访问，您的**Edge密钥**也将显示在此处。

<figure><img src="..//assets/2.18-environments-autoonboarding-type.png" alt=""><figcaption></figcaption></figure>

选择类型后，配置选项并选择平台(Linux或Windows)以生成Edge agent部署脚本。

| 字段/选项                     | 概述                                                                                                                                                       |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Portainer API服务器URL       | 此字段显示您的Portainer API服务器URL。可以在Edge计算设置中调整此值。                                                                                     |
| Portainer隧道服务器地址      | 此字段显示您的Portainer隧道服务器地址。可以在Edge计算设置中调整此值，不用于Edge Agent异步部署。                                                          |
| 组                           | 为您的Edge Agent部署选择一个[组](groups.md)。                                                                                                           |
| Edge组                       | 为您的Edge Agent部署选择一个或多个[Edge组](../../user/edge/groups.md)。                                                                                 |
| 标签                         | 为您的Edge Agent部署选择一个或多个[标签](tags.md)。                                                                                                     |
| Edge ID生成器                | 提供一个单行脚本，用于为您的Edge设备生成唯一ID。对于Linux，示例可以是使用`uuidgen`命令。                                                                |
| 环境变量                     | 定义一个逗号分隔的环境变量列表，这些变量将从Edge设备获取并在Portainer中使用。                                                                           |
| 允许自签名证书               | 切换此选项以允许在Edge Agent和Portainer服务器之间的通信中使用自签名证书。                                                                               |

<figure><img src="..//assets/2.18-environments-autoonboarding-config.png" alt=""><figcaption></figcaption></figure>

选择部署环境并点击**复制**将脚本复制到剪贴板。

<figure><img src="..//assets/2.20-environments-aeec-script.png" alt=""><figcaption></figcaption></figure>
