# 配置服务选项

从菜单中选择**服务**，然后选择要配置的服务。

<figure><img src="../..//assets/2.15-docker_services_configure.gif" alt=""><figcaption></figcaption></figure>

## 服务详情

在此部分您可以：
* 查看服务详情摘要
* 配置副本数量
* 开启/关闭[服务webhook](webhooks.md)
* 查看[服务日志](logs.md)
* 更新、[回滚](rollback.md)或删除服务

<figure><img src="../..//assets/2.15-docker_services_service_details (1).png" alt=""><figcaption></figcaption></figure>

## 容器规格配置选项

### 更改容器镜像

在此可以替换容器镜像。选择注册表，输入镜像名称，然后点击**应用更改**。

<figure><img src="../..//assets/2.15-docker_services_change_container_image.png" alt=""><figcaption></figcaption></figure>

### 环境变量

最好在[创建容器](../containers/add.md)和部署前设置环境变量。如果需要，您仍可以在部署后设置或编辑这些变量。

<figure><img src="../..//assets/2.15-docker_services_service_env_var.png" alt=""><figcaption></figcaption></figure>

### 容器标签

标签让您可以记录有关容器的信息，例如其配置方式。标签也可用于[从界面隐藏容器](../../../admin/settings/#hidden-containers)。

<figure><img src="../..//assets/2.15-docker_services_service_container_labels.png" alt=""><figcaption></figcaption></figure>

### 挂载

您可以选择在Portainer中挂载或绑定卷，也可以将它们设为只读。要添加挂载，首先从**类型**下拉列表中选择**卷**或**绑定**。

#### 对于卷挂载：

从**源**下拉列表中选择卷，在**目标**字段中输入容器路径，如果需要则勾选**只读**，然后点击**应用更改**。

<figure><img src="../..//assets/2.15-docker_services_service_mounts_volume.png" alt=""><figcaption></figcaption></figure>

#### 对于绑定挂载：

在**源**字段中输入源路径，在**目标**字段中输入容器路径，如果需要则勾选**只读**，然后点击**应用更改**。

<figure><img src="../..//assets/2.15-docker_services_service_mounts_bind.png" alt=""><figcaption></figcaption></figure>

## 网络和端口配置选项

### 网络

您可以在部署前后为服务定义一个或多个网络。只需从下拉列表中选择网络，然后点击**应用更改**。

<figure><img src="../..//assets/2.15-docker_services_service_networks.png" alt=""><figcaption></figcaption></figure>

### 发布端口

使用此设置发布端口，以便可以从主机外部访问容器。您可以添加新端口或更新现有端口。

<figure><img src="../..//assets/2.15-docker_services_service_published_ports.png" alt=""><figcaption></figcaption></figure>

### 主机文件条目

让您可以手动指定主机名或URL，并将URL与内部或外部IP地址关联。

<figure><img src="../..//assets/2.15-docker_services_service_host_entries.png" alt=""><figcaption></figcaption></figure>

## 服务规格设置

### 资源限制和保留

设置资源利用限制，如内存、CPU保留和CPU限制。

<figure><img src="../..//assets/2.15-docker_services_service_resource_limits.png" alt=""><figcaption></figcaption></figure>

### 放置约束

使用放置约束控制服务可以分配到哪些节点。

<figure><img src="../..//assets/2.15-docker_services_service_placement_constraint.png" alt=""><figcaption></figcaption></figure>

### 放置偏好

放置约束限制服务可以运行的节点，而放置偏好尝试以算法方式(默认均匀分布)将任务放置在适当的节点上。

<figure><img src="../..//assets/2.15-docker_services_service_placement_pref.png" alt=""><figcaption></figcaption></figure>

### 重启策略

Docker的重启策略确保链接的容器以正确的顺序重启，并控制它们重启的条件：

* **任何情况**：在任何条件下重启容器(重启主机或Docker守护进程)
* **失败时**：如果容器因错误退出(表现为非零退出代码)则重启
* **不重启**：不自动重启容器

您还可以调整重启延迟、最大尝试次数和重启窗口。

<figure><img src="../..//assets/2.15-docker_services_service_restart_policy.png" alt=""><figcaption></figcaption></figure>

### 更新配置

根据您指定的参数更新服务。此处指定的参数与`docker service create`相同(更多信息请参阅[Docker官方文档](https://docs.docker.com/engine/reference/commandline/service_create/))。

通常，更新服务仅会在服务更改需要重新创建任务以使其生效时，才会用新任务替换服务的任务。

<figure><img src="../..//assets/2.15-docker_services_service_update_config.png" alt=""><figcaption></figcaption></figure>

### 日志驱动

Docker包含称为_日志驱动_的日志机制，从您运行的容器和服务中获取信息。每个Docker守护进程都有一个默认的日志驱动，除非您配置它们使用不同的日志驱动，否则每个容器都将使用该驱动。

<figure><img src="../..//assets/2.15-docker_services_service_logging_driver.png" alt=""><figcaption></figcaption></figure>

### 服务标签

让您可以使用Docker标签通过数组或字典向容器添加元数据。我们建议使用反向DNS表示法，以防止标签与其他软件使用的标签冲突。

<figure><img src="../..//assets/2.15-docker_services_service_labels.png" alt=""><figcaption></figcaption></figure>

### 配置

Docker 17.06引入了Swarm服务配置。这些允许您在服务镜像或运行容器之外存储非敏感信息，如配置文件。这使镜像尽可能通用，并消除了将配置文件绑定挂载到容器中或使用环境变量的需要。

<figure><img src="../..//assets/2.15-docker_services_service_configs.png" alt=""><figcaption></figcaption></figure>

### 密钥

在Docker Swarm服务的上下文中，密钥是一段数据，如密码、SSH私钥、SSL证书或其他不应通过网络传输或以未加密形式存储在Dockerfile或应用程序源代码中的数据。

<figure><img src="../..//assets/2.15-docker_services_service_secrets.png" alt=""><figcaption></figcaption></figure>
