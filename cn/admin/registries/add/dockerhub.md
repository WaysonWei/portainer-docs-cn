# 添加DockerHub账户

Portainer提供对Docker Hub匿名访问的内置支持，但在某些情况下您可能需要登录Docker Hub（例如访问私有镜像或支持拉取大量镜像）。

从菜单中选择**注册表**，然后点击**添加注册表**并选择**DockerHub**作为注册表提供商。

<figure><img src="../..//assets/2.15-settings-registries-add-dockerhub.gif" alt=""><figcaption></figcaption></figure>

填写表单，参考下表作为指南。

| 字段/选项           | 概述                                                                                                                                                                                                                                 |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 名称                | 输入注册表的名称。这将显示在注册表列表中以及选择拉取镜像的注册表时。                                                                                                                                                              |
| DockerHub用户名     | 输入用于连接Docker Hub的用户名。                                                                                                                                                                                                   |
| DockerHub访问令牌   | 输入与上述用户名对应的Docker Hub个人访问令牌。您可以通过登录Docker Hub，点击右上角的用户名，进入账户设置然后选择安全选项卡来创建访问令牌。                                                                                        |

<figure><img src="../..//assets/2.15-settings-registries-add-dockerhub-details.png" alt=""><figcaption></figcaption></figure>

表单填写完成后，点击**添加注册表**。
