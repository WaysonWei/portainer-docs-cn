# 详细信息

此页面提供所选环境的Docker Swarm集群信息。页面分为以下部分：集群状态和节点，点击节点名称可跳转到该节点的概览页面。

此页面仅对Docker Swarm环境可用。

## 集群状态

此部分描述集群的基本配置，包括节点数量、Docker API版本以及可用的总CPU和内存。还包含指向[集群可视化](cluster-visualizer.md)的链接。

<figure><img src="../..//assets/2.15-swarm-clusterstatus.png" alt=""><figcaption></figcaption></figure>

## 节点

列出集群中的所有节点以及每个节点的摘要信息，包括：

* 节点角色
* 节点可用的CPU数量和内存
* 节点上运行的Docker Engine版本
* 节点的IP地址
* 节点的状态和可用性

<figure><img src="../..//assets/2.15-swarm-nodes.png" alt=""><figcaption></figcaption></figure>

点击单个节点名称可跳转到该节点的概览页面。

## 节点概览

### 主机详情

此部分描述节点的基本配置，包括主机名、操作系统信息以及总CPU和内存。

<figure><img src="../..//assets/2.15-swarm-nodedetail.png" alt=""><figcaption></figcaption></figure>

### 引擎详情

Docker版本和可用的卷及网络插件等信息，帮助您了解节点上运行的Docker引擎。

<figure><img src="../..//assets/2.15-swarm-nodedetail-engine.png" alt=""><figcaption></figcaption></figure>

### PCI设备和物理磁盘

这些部分列出节点上可用的PCI设备和物理磁盘。

这些部分仅在集群启用了[主机管理功能](setup.md#host-and-filesystem)时可见。

<figure><img src="../..//assets/2.15-docker-host-pci.png" alt=""><figcaption></figcaption></figure>

### 节点详情

此处可找到节点作为集群一部分的配置详情。您可以查看角色、设置节点的可用状态、查看当前状态并为节点应用标签。

<figure><img src="../..//assets/2.15-swarm-nodedetail-detail.png" alt=""><figcaption></figcaption></figure>
