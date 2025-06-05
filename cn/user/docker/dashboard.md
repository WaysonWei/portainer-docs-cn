# 仪表盘

Docker/Swarm仪表盘总结了您的Docker独立或Docker Swarm环境，并显示组成该环境的各个组件。

## 环境信息

此部分仅对Docker独立和Podman环境可见。

此部分显示环境名称、其URL和端口以及任何[标签](../../admin/environments/tags.md#tagging-an-environment)。您还可以看到CPU核心数（及其可用内存）、Docker/Podman版本，以及是否安装了Portainer Agent。

<figure><img src="..//assets/2.15-docker-standalone-dashboard.png" alt=""><figcaption></figcaption></figure>

## 集群信息

此部分仅对Docker Swarm环境可见。

此部分显示集群中的节点数量以及[集群可视化工具](swarm/cluster-visualizer.md)的链接。

<figure><img src="..//assets/2.15-docker-dashboard-swarm.png" alt=""><figcaption></figcaption></figure>

## 摘要磁贴

仪表盘的其余部分由显示[堆栈](stacks/)、[服务](services/)（针对Docker Swarm）、[容器](containers/)（包括健康状态和运行状态指标）、[镜像](images/)（及其占用的磁盘空间）、[卷](volumes/)和[网络](networks/)数量的磁贴组成，以及GPU（如果启用）。

<figure><img src="..//assets/2.15-docker-dashboard-tiles.png" alt=""><figcaption></figcaption></figure>
