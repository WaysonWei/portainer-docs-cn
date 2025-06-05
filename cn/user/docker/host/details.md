# 详情

此页面提供所选环境的Docker主机信息。页面分为以下部分：主机详情、引擎详情以及（如果启用）PCI设备和物理磁盘。

此页面仅适用于Docker独立环境。

## 主机详情

此部分描述主机的基本配置，包括主机名、操作系统信息、内核版本、总CPU和内存。如果环境安装了Portainer Agent，[主机管理功能](setup.md#enable-host-management-features)已启用，并且配置了`/host`挂载，您还可以从此处浏览主机文件系统。

<figure><img src="../..//assets/2.15-docker-host-details.png" alt=""><figcaption></figcaption></figure>

## 引擎详情

了解有关在您的环境上运行的Docker或Podman引擎的更多信息，包括Docker/Podman版本、根目录、存储和日志驱动程序以及可用的卷和网络插件。

<figure><img src="../..//assets/2.15-docker-host-engine.png" alt=""><figcaption></figcaption></figure>

## PCI设备和物理磁盘

这些部分列出了主机上可用的PCI设备和物理磁盘。

这些部分仅在为环境启用[主机管理功能](setup.md#enable-host-management-features)时可见。

<figure><img src="../..//assets/2.15-docker-host-pci.png" alt=""><figcaption></figcaption></figure>
