# 访问控制

所有通过 Portainer 部署的 Docker 和 Docker Swarm 资源（除镜像外）都具有访问控制设置。您可以在部署资源时或之后设置这些控制。通过堆栈或服务部署的资源将继承父级相同的访问权限。

## 通过 Portainer 部署的资源

### 仅管理员访问

这是一个启用访问控制的示例部分。通过这些设置，只有 Portainer 管理员才能访问该资源及其创建的任何其他资源（例如创建容器、服务、卷、网络和机密的堆栈）。

<figure><img src="/assets/2.15-advanced-accesscontrol-admin.png" alt=""><figcaption></figcaption></figure>

### 所有用户可访问

这是一个禁用访问控制的示例部分。所有 Portainer 用户都可以访问该资源及其创建的任何资源。

<figure><img src="/assets/2.15-advanced-accesscontrol-public.png" alt=""><figcaption></figcaption></figure>

### 限制特定团队或用户访问

这是一个在**限制**模式下启用访问控制的示例部分。选择限制选项后，您可以选择更多团队和用户并授予他们访问该资源的权限。

<figure><img src="/assets/2.15-advanced-accesscontrol-restricted.png" alt=""><figcaption></figcaption></figure>

## 在 Portainer 外部部署的资源

任何在 Portainer 外部部署到 Docker 或 Docker Swarm 的资源都将标记为`external`，您对这些资源的控制有限。默认情况下，这些资源将仅限管理员访问，但您可以使用以下标签启用访问控制（示例参数，请替换为您自己的参数）：

| 标签                                       | 授予的访问权限                                                                                                          |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `io.portainer.accesscontrol.public`         | 所有 Portainer 用户均可访问该资源。优先于团队/用户分配。                           |
| `io.portainer.accesscontrol.teams=dev,prod` | 仅限`dev`和`prod`团队访问。可与`io.portainer.accesscontrol.users`结合使用    |
| `io.portainer.accesscontrol.users=bob,adam` | 仅限用户`bob`和`adam`访问。可与`io.portainer.accesscontrol.teams`结合使用 |

### 示例 1 <a href="#examples" id="examples"></a>

使用 Docker Compose 部署堆栈并限制`dev`和`prod`团队访问：

```
version: '3.2'
services:
    ltest:
        image: busybox:latest
        command: "ping localhost"
        labels:
            io.portainer.accesscontrol.teams: dev,prod
```

### 示例 2

使用 Docker CLI 部署堆栈并限制`testers`团队及用户`bob`和`adam`访问：

```
version: '3.2'
services:
    ltest:
        image: busybox:latest
        command: "ping localhost"
        labels:
            io.portainer.accesscontrol.teams: testers
            io.portainer.accesscontrol.users: bob,adam
```

### 示例 3

使用 Docker CLI 部署容器并允许所有 Portainer 用户访问：

```
docker run -d --label io.portainer.accesscontrol.public nginx:latest
```

### 示例 4

使用 Docker CLI 部署容器并限制`dev`和`prod`团队及用户`bob`访问：

```
docker run -d --label io.portainer.accesscontrol.teams=dev,prod --label io.portainer.accesscontrol.users=bob nginx:latest
