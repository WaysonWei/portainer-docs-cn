# 目录

* [欢迎](README.md)
* [2.27版本新功能](whats-new.md)
* [发布说明](release-notes.md)

## 入门指南 <a href="#start" id="start"></a>

* [介绍](start/intro.md)
* [Portainer架构](start/architecture.md)
* [生命周期策略](start/lifecycle.md)
* [系统要求和前提条件](start/requirements-and-prerequisites.md)
* [安装Portainer BE](start/install/README.md)
  * [设置新的Portainer BE服务器安装](start/install/server/README.md)
    * [Docker Standalone](start/install/server/docker/README.md)
      * [在Linux上使用Docker安装Portainer BE](start/install/server/docker/linux.md)
      * [在WSL/Docker Desktop上使用Docker安装Portainer BE](start/install/server/docker/wsl.md)
      * [在Windows容器服务上使用Docker安装Portainer BE](start/install/server/docker/wcs.md)
    * [Docker Swarm](start/install/server/swarm/README.md)
      * [在Linux上使用Docker Swarm安装Portainer BE](start/install/server/swarm/linux.md)
      * [在WSL/Docker Desktop上使用Docker Swarm安装Portainer BE](start/install/server/swarm/wsl.md)
      * [在Windows容器服务上使用Docker Swarm安装Portainer BE](start/install/server/swarm/wcs.md)
    * [Podman](start/install/server/podman/README.md)
      * [在Linux上使用Podman安装Portainer BE](start/install/server/podman/linux.md)
    * [Kubernetes](start/install/server/kubernetes/README.md)
      * [在Kubernetes环境中安装Portainer BE](start/install/server/kubernetes/baremetal.md)
      * [在WSL/Docker Desktop上使用Kubernetes安装Portainer BE](start/install/server/kubernetes/wsl.md)
    * [初始设置](start/install/server/setup.md)
* [安装Portainer CE](start/install-ce/README.md)
  * [设置新的Portainer CE服务器安装](start/install-ce/server/README.md)
    * [Docker Standalone](start/install-ce/server/docker/README.md)
      * [在Linux上使用Docker安装Portainer CE](start/install-ce/server/docker/linux.md)
      * [在WSL/Docker Desktop上使用Docker安装Portainer CE](start/install-ce/server/docker/wsl.md)
      * [在Windows容器服务上使用Docker安装Portainer CE](start/install-ce/server/docker/wcs.md)
    * [Docker Swarm](start/install-ce/server/swarm/README.md)
      * [在Linux上使用Docker Swarm安装Portainer CE](start/install-ce/server/swarm/linux.md)
      * [在WSL/Docker Desktop上使用Docker Swarm安装Portainer CE](start/install-ce/server/swarm/wsl.md)
      * [在Windows容器服务上使用Docker Swarm安装Portainer CE](start/install-ce/server/swarm/wcs.md)
    * [Podman](start/install-ce/server/podman/README.md)
      * [在Linux上使用Podman安装Portainer CE](start/install-ce/server/podman/linux.md)
    * [Kubernetes](start/install-ce/server/kubernetes/README.md)
      * [在Kubernetes环境中安装Portainer CE](start/install-ce/server/kubernetes/baremetal.md)
      * [在WSL/Docker Desktop上使用Kubernetes安装Portainer CE](start/install-ce/server/kubernetes/wsl.md)
    * [初始设置](start/install-ce/server/setup.md)
* [向现有安装添加环境](start/agent.md)
* [更新Portainer](start/upgrade/README.md)
  * [在Docker Standalone上更新](start/upgrade/docker.md)
  * [在Docker Swarm上更新](start/upgrade/swarm.md)
  * [在Podman上更新](start/upgrade/podman.md)
  * [在Kubernetes上更新](start/upgrade/kubernetes.md)
  * [在Nomad上更新](start/upgrade/nomad.md)
  * [更新Edge Agent](start/upgrade/edge.md)
  * [从Portainer 1.x更新](start/upgrade/from-1.x.md)
  * [切换到Portainer商业版](start/upgrade/tobe/README.md)
    * [从Portainer社区版内部升级到商业版](start/upgrade/tobe/inapp.md)
    * [Docker Standalone](start/upgrade/tobe/docker.md)
    * [Docker Swarm](start/upgrade/tobe/swarm.md)
    * [Podman](start/upgrade/tobe/podman.md)
    * [Kubernetes](start/upgrade/tobe/kubernetes.md)
    * [升级仅Agent部署](start/upgrade/tobe/agent.md)

## 使用Portainer <a href="#user" id="user"></a>

* [首页](user/home/README.md)
  * [快照浏览](user/home/snapshot.md)
  * [OpenAMT](user/home/openamt.md)
* [Docker/Swarm/Podman](user/docker/README.md)
  * [仪表盘](user/docker/dashboard.md)
  * [模板](user/docker/templates/README.md)
    * [应用](user/docker/templates/application.md)
    * [自定义模板](user/docker/templates/custom.md)
    * [部署堆栈](user/docker/templates/deploy-stack.md)
    * [部署容器](user/docker/templates/deploy-container.md)
  * [堆栈](user/docker/stacks/README.md)
    * [添加新堆栈](user/docker/stacks/add.md)
    * [检查或编辑堆栈](user/docker/stacks/edit.md)
    * [从已部署堆栈创建模板](user/docker/stacks/template.md)
    * [Webhooks](user/docker/stacks/webhooks.md)
    * [迁移或复制堆栈](user/docker/stacks/migrate.md)
    * [移除堆栈](user/docker/stacks/remove.md)
  * [服务](user/docker/services/README.md)
    * [添加新服务](user/docker/services/add.md)
    * [配置服务选项](user/docker/services/configure.md)
    * [扩展服务](user/docker/services/scale.md)
    * [查看服务任务状态](user/docker/services/tasks.md)
    * [查看服务日志](user/docker/services/logs.md)
    * [回滚服务](user/docker/services/rollback.md)
    * [Webhooks](user/docker/services/webhooks.md)
  * [容器](user/docker/containers/README.md)
    * [添加新容器](user/docker/containers/add.md)
    * [查看容器详情](user/docker/containers/view.md)
    * [检查容器](user/docker/containers/inspect.md)
    * [编辑或复制容器](user/docker/containers/edit.md)
    * [高级容器设置](user/docker/containers/advanced.md)
    * [Webhooks](user/docker/containers/webhooks.md)
    * [附加卷到容器](user/docker/containers/attach-volume.md)
    * [查看容器日志](user/docker/containers/logs.md)
    * [查看容器统计信息](user/docker/containers/stats.md)
    * [访问容器控制台](user/docker/containers/console.md)
    * [更改容器所有权](user/docker/containers/ownership.md)
    * [移除容器](user/docker/containers/remove.md)
  * [镜像](user/docker/images/README.md)
    * [拉取镜像](user/docker/images/pull.md)
    * [构建新镜像](user/docker/images/build.md)
    * [导入镜像](user/docker/images/import.md)
    * [导出镜像](user/docker/images/export.md)
  * [网络](user/docker/networks/README.md)
    * [添加新网络](user/docker/networks/add.md)
    * [移除网络](user/docker/networks/remove.md)
  * [卷](user/docker/volumes/README.md)
    * [添加新卷](user/docker/volumes/add.md)
    * [浏览卷](user/docker/volumes/browse.md)
    * [移除卷](user/docker/volumes/remove.md)
  * [配置](user/docker/configs/README.md)
    * [添加新配置](user/docker/configs/add.md)
    * [移除配置](user/docker/configs/remove.md)
  * [密钥](user/docker/secrets/README.md)
    * [添加新密钥](user/docker/secrets/add.md)
    * [移除密钥](user/docker/secrets/remove.md)
  * [事件](user/docker/events.md)
  * [主机](user/docker/host/README.md)
    * [详情](user/docker/host/details.md)
    * [设置](user/docker/host/setup.md)
    * [注册表](user/docker/host/registries.md)
  * [Swarm](user/docker/swarm/README.md)
    * [详情](user/docker/swarm/details.md)
    * [集群可视化工具](user/docker/swarm/cluster-visualizer.md)
    * [设置](user/docker/swarm/setup.md)
    * [注册表](user/docker/swarm/registries.md)
* [Kubernetes](user/kubernetes/README.md)
  * [仪表盘](user/kubernetes/dashboard.md)
  * [kubectl shell](user/kubernetes/kubectl.md)
  * [Kubeconfig](user/kubernetes/kubeconfig.md)
  * [自定义模板](user/kubernetes/templates/README.md)
    * [添加新自定义模板](user/kubernetes/templates/add.md)
    * [编辑自定义模板](user/kubernetes/templates/edit.md)
    * [移除自定义模板](user/kubernetes/templates/remove.md)
  * [命名空间](user/kubernetes/namespaces/README.md)
    * [添加新命名空间](user/kubernetes/namespaces/add.md)
    * [管理命名空间](user/kubernetes/namespaces/manage.md)
    * [管理命名空间访问权限](user/kubernetes/namespaces/access.md)
    * [移除命名空间](user/kubernetes/namespaces/remove.md)
  * [Helm](user/kubernetes/helm.md)
  * [应用](user/kubernetes/applications/README.md)
    * [使用表单添加新应用](user/kubernetes/applications/add.md)
    * [使用代码添加新应用](user/kubernetes/applications/manifest.md)
    * [检查应用](user/kubernetes/applications/inspect.md)
    * [检查Helm应用](user/kubernetes/applications/inspect-helm.md)
    * [编辑应用](user/kubernetes/applications/edit.md)
    * [Webhooks](user/kubernetes/applications/webhooks.md)
    * [从应用分离卷](user/kubernetes/applications/detach-volume.md)
    * [移除应用](user/kubernetes/applications/remove.md)
  * [网络](user/kubernetes/networking/README.md)
    * [服务](user/kubernetes/networking/services.md)
    * [Ingresses](user/kubernetes/networking/ingresses/README.md)
      * [手动添加Ingress](user/kubernetes/networking/ingresses/add.md)
      * [使用清单添加Ingress](user/kubernetes/networking/ingresses/manifest.md)
      * [移除Ingress](user/kubernetes/networking/ingresses/remove-an-ingress.md)
  * [ConfigMaps与Secrets](user/kubernetes/configurations/README.md)
    * [添加ConfigMap](user/kubernetes/configurations/add.md)
    * [添加Secret](user/kubernetes/configurations/add-1.md)
  * [卷](user/kubernetes/volumes/README.md)
    * [检查卷](user/kubernetes/volumes/inspect.md)
    * [移除卷](user/kubernetes/volumes/remove.md)
  * [更多资源](user/kubernetes/more-resources/README.md)
    * [Cron Jobs与Jobs](user/kubernetes/more-resources/jobs.md)
    * [服务账户](user/kubernetes/more-resources/service-accounts.md)
    * [集群角色](user/kubernetes/more-resources/cluster-roles.md)
    * [角色](user/kubernetes/more-resources/namespace-roles.md)
  * [集群](user/kubernetes/cluster/README.md)
    * [详情](user/kubernetes/cluster/details.md)
    * [检查节点](user/kubernetes/cluster/node.md)
    * [设置](user/kubernetes/cluster/setup.md)
    * [安全约束](user/kubernetes/cluster/security.md)
    * [注册表](user/kubernetes/cluster/registries.md)
* [Azure ACI](user/aci/README.md)
  * [仪表盘](user/aci/dashboard.md)
  * [容器实例](user/aci/containers/README.md)
    * [添加新容器](user/aci/containers/add.md)
    * [查看容器详情](user/aci/containers/details.md)
    * [移除容器](user/aci/containers/remove.md)
* [Nomad](user/nomad.md)
* [边缘计算](user/edge/README.md)
  * [边缘组](user/edge/groups.md)
  * [边缘堆栈](user/edge/stacks/README.md)
    * [添加新边缘堆栈](user/edge/stacks/add.md)
  * [边缘作业](user/edge/jobs.md)
  * [边缘配置](user/edge/configurations.md)
  * [等待室](user/edge/waiting-room.md)
  * [边缘模板](user/edge/templates/README.md)
    * [应用](user/edge/templates/application.md)
    * [自定义](user/edge/templates/custom.md)
* [账户设置](user/account-settings.md)

## 管理Portainer <a href="#admin" id="admin"></a>

* [用户相关](admin/user/README.md)
  * [用户](admin/user/users.md)
  * [添加新用户](admin/user/add.md)
  * [将用户提升为管理员](admin/user/promote.md)
  * [重置用户密码](admin/user/password.md)
  * [团队](admin/user/teams/README.md)
    * [添加新团队](admin/user/teams/add.md)
    * [将用户添加到团队](admin/user/teams/add-user.md)
  * [角色](admin/user/roles.md)
* [环境相关](admin/environments/README.md)
  * [环境](admin/environments/environments.md)
  * [添加新环境](admin/environments/add/README.md)
    * [添加本地环境](admin/environments/add/local.md)
    * [添加Docker Standalone环境](admin/environments/add/docker/README.md)
      * [在Docker Standalone上安装Portainer Agent](admin/environments/add/docker/agent.md)
      * [连接到Docker API](admin/environments/add/docker/api.md)
      * [连接到Docker Socket](admin/environments/add/docker/socket.md)
      * [在Docker Standalone上安装Edge Agent标准版](admin/environments/add/docker/edge.md)
      * [在Docker Standalone上安装Edge Agent异步版](admin/environments/add/docker/edge-async.md)
    * [添加Docker Swarm环境](admin/environments/add/swarm/README.md)
      * [在Docker Swarm上安装Portainer Agent](admin/environments/add/swarm/agent.md)
      * [连接到Docker API](admin/environments/add/swarm/api.md)
      * [连接到Docker Socket](admin/environments/add/swarm/socket.md)
      * [在Docker Swarm上安装Edge Agent标准版](admin/environments/add/swarm/edge.md)
      * [在Docker Swarm上安装Edge Agent异步版](admin/environments/add/swarm/edge-async.md)
    * [添加Podman环境](admin/environments/add/podman/README.md)
      * [在Podman上安装Portainer Agent](admin/environments/add/podman/agent.md)
      * [连接到Podman Socket](admin/environments/add/podman/socket.md)
      * [在Podman上安装Edge Agent标准版](admin/environments/add/podman/edge.md)
      * [在Podman上安装Edge Agent异步版](admin/environments/add/podman/edge-async.md)
    * [添加Kubernetes环境](admin/environments/add/kubernetes/README.md)
      * [在Kubernetes环境中安装Portainer Agent](admin/environments/add/kubernetes/agent.md)
      * [在Kubernetes上安装Edge Agent标准版](admin/environments/add/kubernetes/edge.md)
      * [在Kubernetes上安装Edge Agent异步版](admin/environments/add/kubernetes/edge-async.md)
      * [导入现有Kubernetes环境](admin/environments/add/kubernetes/import.md)
    * [添加ACI环境](admin/environments/add/aci.md)
    * [添加Nomad环境](admin/environments/add/nomad.md)
    * [配置KaaS集群](admin/environments/add/kaas/README.md)
      * [Civo](admin/environments/add/kaas/civo.md)
      * [Akamai Connected Cloud](admin/environments/add/kaas/linode.md)
      * [DigitalOcean](admin/environments/add/kaas/digitalocean.md)
      * [Google Cloud](admin/environments/add/kaas/gke.md)
      * [AWS](admin/environments/add/kaas/eks.md)
      * [Azure](admin/environments/add/kaas/aks.md)
    * [创建Kubernetes集群](admin/environments/add/kube-create/README.md)
      * [Talos Kubernetes](admin/environments/add/kube-create/omni.md)
      * [MicroK8s](admin/environments/add/kube-create/microk8s/README.md)
        * [离线安装](admin/environments/add/kube-create/microk8s/offline.md)
    * [通过Portainer API添加环境](admin/environments/add/api.md)
  * [自动加入](admin/environments/aeec.md)
  * [组](admin/environments/groups.md)
  * [标签](admin/environments/tags.md)
  * [管理环境访问权限](admin/environments/access.md)
  * [管理环境组访问权限](admin/environments/access-groups.md)
  * [更新与回滚](admin/environments/update.md)
* [注册表](admin/registries/README.md)
  * [添加新注册表](admin/registries/add/README.md)
    * [添加DockerHub账户](admin/registries/add/dockerhub.md)
    * [添加AWS ECR注册表](admin/registries/add/ecr.md)
    * [添加Quay.io注册表](admin/registries/add/quay.md)
    * [添加ProGet注册表](admin/registries/add/proget.md)
    * [添加Azure注册表](admin/registries/add/azure.md)
    * [添加Gitlab注册表](admin/registries/add/gitlab.md)
    * [添加GitHub注册表](admin/registries/add/ghcr.md)
    * [添加自定义注册表](admin/registries/add/custom.md)
  * [浏览注册表](admin/registries/browse.md)
  * [管理注册表](admin/registries/manage.md)
* [许可证](admin/licenses.md)
* [日志](admin/logs/README.md)
  * [认证](admin/logs/authentication.md)
  * [活动](admin/logs/activity.md)
* [通知](admin/notifications.md)
* [设置](admin/settings/README.md)
  * [常规](admin/settings/general.md)
  * [认证](admin/settings/authentication/README.md)
    * [通过LDAP认证](admin/settings/authentication/ldap.md)
    * [通过Active Directory认证](admin/settings/authentication/active-directory.md)
    * [通过OAuth认证](admin/settings/authentication/oauth.md)
  * [共享凭据](admin/settings/credentials/README.md)
    * [添加Sidero Omni凭据](admin/settings/credentials/omni.md)
    * [添加Civo凭据](admin/settings/credentials/civo.md)
    * [添加Akamai Connected Cloud凭据](admin/settings/credentials/linode.md)
    * [添加DigitalOcean凭据](admin/settings/credentials/digitalocean.md)
    * [添加Google Cloud凭据](admin/settings/credentials/gke.md)
    * [添加AWS凭据](admin/settings/credentials/eks.md)
    * [添加Azure凭据](admin/settings/credentials/aks.md)
    * [添加SSH凭据](admin/settings/credentials/ssh.md)
  * [边缘计算](admin/settings/edge.md)

## 常见问题 <a href="#faq" id="faq"></a>

* [Portainer概念](faq/concepts.md)
* [安装](faq/installing.md)
* [升级](faq/upgrading.md)
* [故障排除](faq/troubleshooting.md)
* [贡献](faq/contributing.md)

## 高级主题 <a href="#advanced" id="advanced"></a>

* [CLI配置选项](advanced/cli.md)
* [应用模板](advanced/app-templates/README.md)
  * [构建和托管自己的应用模板](advanced/app-templates/build.md)
  * [应用模板JSON格式](advanced/app-templates/format.md)
* [Portainer Edge Agent](advanced/edge-agent.md)
* [访问控制](advanced/access-control.md)
* [重置管理员密码](advanced/reset-admin.md)
* [安全与合规](advanced/security.md)
* [加密Portainer数据库](advanced/db-encryption.md)
* [使用自定义SSL证书](advanced/ssl.md)
* [使用mTLS与Portainer](advanced/mtls.md)
* [将认证和活动日志流式传输到外部提供商](advanced/siem.md)
* [将Portainer与反向代理一起使用](advanced/reverse-proxy/README.md)
  * [在Traefik Proxy后部署Portainer](advanced/reverse-proxy/traefik.md)
  * [在nginx反向代理后部署Portainer](advanced/reverse-proxy/nginx.md)
* [Portainer中相对路径支持的工作原理](advanced/relative-paths.md)
* [Helm图表配置选项](advanced/helm-chart-configuration-options.md)
* [Docker角色和权限](advanced/docker-roles-and-permissions.md)
* [Kubernetes角色和绑定](advanced/kubernetes-roles-and-bindings.md)
* [已弃用和移除的功能](advanced/deprecated.md)

## API

* [访问Portainer API](api/access.md)
* [API文档](api/docs.md)
* [API使用示例](api/examples.md)

## 获取更多帮助 <a href="#help" id="help"></a>

* [知识库](https://portal.portainer.io/knowledge)
* [Portainer学院](https://academy.portainer.io)
* [YouTube](https://www.youtube.com/channel/UC7diMJcrULjDseq5yhSUZgg/videos)
* [GitHub](https://github.com/orgs/portainer/discussions)
* [Slack](https://join.slack.com/t/portainer/shared_invite/zt-21zpww5ab-mG_lA7UXbWL3HW3sPqjqEA)
* [Discord](https://discord.com/invite/j8fVken)
* [提交支持请求](https://www.portainer.io/portainer-business-support)

## 贡献给Portainer <a href="#contribute" id="contribute"></a>

* [贡献](contribute/contribute.md)
* [构建说明](contribute/build/README.md)
  * [设置macOS构建环境](contribute/build/mac.md)
  * [设置Linux构建环境](contribute/build/linux.md)
