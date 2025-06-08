# 密钥

密钥菜单仅适用于Docker Swarm环境。

密钥是一段数据，如密码、SSH私钥、SSL证书或其他不应通过网络传输、不应以未加密形式存储在Dockerfile中或不应存储在应用程序源代码中的数据。在Docker 1.13及更高版本中，您可以使用Docker密钥集中管理这些数据，并仅安全地传输给需要访问这些数据的容器。

<figure><img src="../..//assets/2.15-docker_secrets_secrets_list.png" alt=""><figcaption></figcaption></figure>

密钥在传输过程中和在Docker Swarm中静态存储时都是加密的。给定的密钥只能被明确授予访问权限的服务访问，并且仅在这些服务任务运行时才能访问。

您可以使用密钥管理容器在运行时需要的任何敏感数据，但您不希望将其存储在镜像或源代码控制中，例如：

* 用户名和密码
* TLS证书和密钥
* SSH密钥
* 其他重要数据，如数据库名称或内部服务器名称
* 通用字符串或二进制内容(最大500Kb大小)

对于不太敏感的数据或更大的内容，请参阅[配置](../configs/)。

在Portainer中，您可以添加和删除密钥以用于部署。

[add.md](add.md)

[remove.md](remove.md)
