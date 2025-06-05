# 配置

**配置**菜单仅对Docker Swarm环境可用。

Docker 17.06引入了swarm服务配置，允许您在服务镜像或运行容器之外存储非敏感信息，如配置文件。这使您可以保持镜像尽可能通用，无需将配置文件绑定挂载到容器中或使用环境变量。[密钥](../secrets/)是存储敏感信息的另一种选择。

<figure><img src="../..//assets/2.15-docker_configs_config_list.png" alt=""><figcaption></figcaption></figure>

在Portainer中，您可以添加和移除用于部署的自定义配置。

[add.md](add.md)

[remove.md](remove.md)
