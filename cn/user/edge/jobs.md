# Edge作业

这是一个测试版功能。

添加Edge作业是在Edge主机上调度作业的好方法。作业可用于运行您需要的任何脚本，例如在指定时间段内运行备份。

此功能需要您[启用边缘计算](../../admin/settings/edge.md)功能，目前仅适用于使用`/etc/cron.d`进行作业调度的Docker独立环境。

Edge作业通过修改底层主机上的crontab运行，而不是在容器中。这意味着Edge作业可以直接对主机进行更改，这非常强大但也非常危险，因此请谨慎使用。

从菜单中选择**Edge作业**，然后点击**添加Edge作业**。

<figure><img src="..//assets/2.15-edge-jobs.gif" alt=""><figcaption></figcaption></figure>

为作业指定一个描述性名称，然后选择以下选项之一：

| 选项                 | 概述                         |
| ---------------------- | -------------------------------- |
| 基本配置    | 从日历中选择日期。 |
| 高级配置 | 编写您自己的`cron`规则。      |

如果选择**重复Edge作业**，还需输入**Edge作业时间**。

Edge作业时间基于主机上的时间，而不是Portainer Server的时间。在跨时区调度作业时请记住这一点。

<figure><img src="..//assets/2.15-edge-jobs-config.png" alt=""><figcaption></figcaption></figure>

然后您可以使用网页编辑器编写脚本或粘贴脚本内容。

脚本准备好后，您可以选择部署位置。您可以使用**Edge组**下拉菜单选择要部署到的[Edge组](groups.md)。

<figure><img src="..//assets/2.17-edge-jobs-groups.png" alt=""><figcaption></figcaption></figure>

您还可以在**目标环境**中单独选择环境。点击**可用环境**列表中的环境可将其移动到**关联环境**列表作为部署目标。

<figure><img src="..//assets/2.15-edge-jobs-targetenvs.png" alt=""><figcaption></figcaption></figure>

完成选择后，点击**创建Edge作业**来创建并运行作业。
