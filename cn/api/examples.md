# API 使用示例

Portainer 提供了一个 HTTP API，您可以通过它来自动化所有通过 Portainer UI 执行的操作。您还可以将 Portainer 作为底层 Docker/Kubernetes API 的网关（通过 Portainer API 发起 HTTP 查询）。

以下示例使用 [httpie](https://httpie.org/) 执行针对 Portainer 的 API 调用。

## 初始化管理员密码

在新安装的 Portainer 上，您需要创建一个管理员账户来初始化 Portainer。首次访问 Portainer URL 时会要求您进行此操作。您也可以通过以下 API 调用实现相同效果：

```
http POST <portainer url>/api/users/admin/init Username="<admin username>" Password="<adminpassword>"
```

## 使用管理员账户进行 API 认证

```
http POST <portainer url>/api/auth Username="<admin username>" Password="<adminpassword>"
```

响应是一个包含 `jwt` 字段中 JWT 令牌的 JSON 对象。执行 API 认证查询时，您需要在授权头中传递此令牌。

```
{
  "jwt":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE"
}
```

授权头的值必须采用 `Bearer <JWT_TOKEN>` 的形式：

```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE
```

此令牌有效期为 8 小时。过期后，您需要生成新令牌才能执行认证查询。

## 添加新环境

新安装的 Portainer 没有配置任何环境。您首先需要添加一个环境供 Portainer 管理。

您可以通过 [Portainer API](../admin/environments/add/api.md) 或通过 Web 界面（在初始设置期间和设置完成后均可）添加要管理的环境。

## 针对特定环境执行 Docker 查询

Portainer HTTP API 端点充当 Docker HTTP API 的反向代理，可用于执行任何 Docker HTTP API 请求：

`/api/endpoints/<ENVIRONMENT_ID>/docker`

阅读 [Docker API 文档](https://docs.docker.com/engine/api/) 了解如何查询 Docker 引擎。

### **列出所有容器**

此调用列出特定环境中所有可用的容器：

```
http GET <portainer url>/api/endpoints/1/docker/containers/json \
    X-API-Key:your_access-token \
    all==true
```

响应与 Docker API 的 `ContainerList` 操作返回的相同。请参阅 [Docker 关于此操作的文档](https://docs.docker.com/engine/api/v1.41/#operation/ContainerList)。

### **创建容器**

您可以使用 Portainer HTTP API 作为网关在特定环境中创建容器。以下查询将在 ID 为 1 的环境中创建一个新的 Docker 容器。容器将被命名为 `web01` 并使用 `nginx:latest` Docker 镜像。它将在主机的 8080 端口上发布容器的 80 端口。

```
http POST <portainer url>/api/endpoints/1/docker/containers/create \
    X-API-Key:your_access-token \
    name=="web01" Image="nginx:latest" \
    ExposedPorts:='{ "80/tcp": {} }' \
    HostConfig:='{ "PortBindings": { "80/tcp": [{ "HostPort": "8080" }] } }'
```

响应与 Docker API 的 `ContainerCreate` 操作返回的相同。请参阅 [Docker 关于此操作的文档](https://docs.docker.com/engine/api/v1.41/#operation/ContainerCreate)。

以下是示例响应：

```
{
    "Id": "5fc2a93d7a3d426a1c3937436697fc5e5343cc375226f6110283200bede3b107",
    "Warnings": null
}
```

您需要容器 ID 才能对该容器执行操作。

### **启动容器**

使用之前获取的 ID，您可以通过以下端点启动新容器：

`/api/endpoints/<ENVIRONMENT_ID>/docker/containers/<CONTAINER_ID>/start`

```
http POST <portainer url>/api/endpoints/1/docker/containers/5fc2a93d7a3d426a1c3937436697fc5e5343cc375226f6110283200bede3b107/start \
    X-API-Key:your_access-token
```

响应与 Docker API 的 `ContainerStart` 操作返回的相同。请参阅 [Docker 关于此操作的文档](https://docs.docker.com/engine/api/v1.41/#operation/ContainerStart)。

### **删除容器**

您可以使用端点 `/api/endpoints/<ENVIRONMENT_ID>/docker/containers/` 删除容器：

```
http DELETE <portainer url>/api/endpoints/1/docker/containers/5fc2a93d7a3d426a1c3937436697fc5e5343cc375226f6110283200bede3b107 \
    X-API-Key:your_access-token \
    force==true
```

响应与 Docker API 的 `ContainerDelete` 操作返回的相同。请参阅 [Docker 关于此操作的文档](https://docs.docker.com/engine/api/v1.41/#operation/ContainerDelete)。
