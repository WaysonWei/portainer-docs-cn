# 管理命名空间访问权限

在Portainer中管理命名空间访问权限之前，必须启用并配置好Kubernetes基于角色的访问控制(RBAC)。

从菜单中选择**命名空间**，然后在要管理的命名空间所在行选择**管理访问**。

<figure><img src="../..//assets/2.20-namespaces-access.gif" alt=""><figcaption></figcaption></figure>

选择将拥有访问权限的用户/团队，然后点击**创建访问**。

具有集群范围角色(如Operator角色)的用户或组不能被分配到单个命名空间，因为它们的集群范围特性适用于环境中的所有命名空间。

<figure><img src="../..//assets/2.20-namespaces-access-create.png" alt=""><figcaption></figcaption></figure>
