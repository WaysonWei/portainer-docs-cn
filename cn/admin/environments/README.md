# 环境相关

在Portainer术语中，_环境_是您希望通过Portainer管理的实例。环境可以是Docker、Docker Swarm、Kubernetes、ACI或它们的组合。一个Portainer Server实例可以管理多个环境。

在2.10版本中，端点(Endpoints)被重命名为环境(Environments)。

[environments.md](environments.md)

[add](add/)

环境可以按组组织并添加标签。

[groups.md](groups.md)

[tags.md](tags.md)

然后可以按每个环境或每个环境组管理访问权限。

[access.md](access.md)

[access-groups.md](access-groups.md)

可以为大型Edge Agent部署生成自动加入脚本。

[aeec.md](aeec.md)

Edge Agent环境可以直接从Portainer内部更新(并回滚更新)。

[update.md](update.md)
