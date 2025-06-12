# 数据卷

数据卷是一个可以挂载到容器中以提供持久化存储的数据存储区域。与绑定挂载不同，数据卷独立于底层操作系统，完全由 Docker Engine 管理。

<figure><img src="../..//assets/2.15-docker_volumes_volumes.png" alt=""><figcaption></figcaption></figure>

带有 **external** 标志的数据卷是在 Portainer 外部创建的，这意味着 Portainer 对其的了解程度低于在 Portainer 内部创建的数据卷。**unused** 标签表示 Portainer 无法看到任何正在使用此数据卷的应用程序。由于可用信息有限，此标签也可能出现在 **external** 资源上。

在 Portainer 中，您可以查看环境中数据卷的列表，添加新数据卷或删除现有数据卷。


[add.md](add.md)
