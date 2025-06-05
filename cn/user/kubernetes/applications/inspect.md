# 检查应用

要查看集群中运行的应用信息，从菜单选择**应用**然后选择要检查的应用。

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect.gif" alt=""><figcaption></figcaption></figure>

**应用详情**屏幕分为四个部分。以下表格解释了每个部分中的所有信息。

## 应用标签页

| 属性        | 概述                                                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 名称             | 应用的名称。                                                                                                         |
| 堆栈            | 应用所属的堆栈(如果有)。                                                                                  |
| 命名空间        | 应用运行的命名空间。                                                                                    |
| 应用类型 | 应用类型(Pod、Deployment、StatefulSet、DaemonSet等)。                                                              |
| 状态           | 指示应用是否正在运行。在适用的情况下，还显示复制状态和副本数。 |
| 创建时间         | 显示应用创建时间、创建者以及应用部署方式。                                     |
| 备注             | 添加或编辑关于应用的备注。                                                                           |

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect-application.png" alt=""><figcaption></figcaption></figure>

## 放置标签页

在此可以找到为应用定义的任何放置约束或偏好信息，以及它们如何被应用。

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect-placement.png" alt=""><figcaption></figcaption></figure>

## 事件标签页

显示与应用相关的事件信息。

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect-events.png" alt=""><figcaption></figcaption></figure>

## YAML标签页

显示从应用部署生成的YAML，并允许直接编辑应用的YAML。此处对manifest的更新使用Kubernetes`patch`机制应用。

通过此部分编辑YAML仅在Portainer商业版中可用。

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect-yaml.png" alt=""><figcaption></figcaption></figure>

进行编辑后点击**应用更改**更新部署。

对于标记为系统的命名空间中的资源，无法编辑YAML。

## 操作

根据应用部署方式，可以执行多种操作，包括：

* [编辑应用](edit.md)
* 执行应用的滚动重启(仅限商业版)
* 重新部署应用(终止所有服务并重新创建)
* 将应用回滚到先前的配置
* 从应用创建[模板](../templates/)

使用Git仓库时，滚动重启和重新部署选项不会从上游仓库重新拉取manifest。要执行此操作，在[编辑应用](edit.md#method-1-redeploy-from-git)时使用**拉取并更新应用**按钮。

<figure><img src="../..//assets/2.17-k8s-applications-inspect-actions.png" alt=""><figcaption><p>可能为您的应用显示的部分操作</p></figcaption></figure>

### 配置详情

| 配置                                | 概述                                                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| 访问应用                    | 显示从容器发布的端口(如果有)。                                            |
| 自动扩展                                 | 指示应用的自动扩展策略。                                                        |
| 环境变量、ConfigMaps或Secrets | 为应用定义的任何环境变量、ConfigMaps和secrets的列表。 |
| 数据持久性                             | 持久化文件夹及其详情的列表。                                                     |

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect-configdetails.png" alt=""><figcaption></figcaption></figure>

## 应用容器

查看哪些pod运行您的应用、使用的镜像、状态、节点和pod的IP地址，以及每个pod的创建时间。还可以从此处访问pod统计信息、控制台和日志。

<figure><img src="../..//assets/2.20-kubernetes-applications-inspect-appcontainers.png" alt=""><figcaption></figcaption></figure>
