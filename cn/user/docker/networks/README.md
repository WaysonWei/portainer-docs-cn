# 网络

Portainer允许您添加、删除和管理环境中的网络。

<figure><img src="../..//assets/2.20-networks-list.png" alt=""><figcaption></figcaption></figure>

[add.md](add.md)

[remove.md](remove.md)

## 支持的网络类型

Portainer支持以下类型的网络：

### bridge

如果不指定驱动，默认会创建此类型网络。桥接网络通常用于需要相互通信的独立容器应用。

### macvlan

macvlan网络允许您为容器分配MAC地址，使其在网络上显示为物理设备。Docker守护进程根据MAC地址将流量路由到容器。当处理期望直接连接到物理网络而非通过Docker主机网络栈路由的传统应用时，使用macvlan驱动有时是最佳选择。

### ipvlan

与macvlan类似，关键区别在于端点具有相同的MAC地址。ipvlan支持L2和L3模式。在ipvlan L2模式下，每个端点获得相同的MAC地址但不同的IP地址。在ipvlan L3模式下，数据包在端点之间路由，提供更好的可扩展性。

### overlay

overlay网络连接多个Docker守护进程，使swarm服务能够相互通信。您还可以使用overlay网络促进swarm服务与独立容器之间，或不同Docker守护进程上的两个独立容器之间的通信。
