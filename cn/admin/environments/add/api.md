# 通过Portainer API添加环境

Portainer的[API](../../../api/docs.md)允许您执行与Portainer UI相同的操作，包括添加新环境。本文介绍如何通过API添加以下类型的环境：

* 使用Docker socket通信的本地环境
* 使用TCP通信的远程环境
* 使用TLS保护的TCP通信的远程环境

本文示例使用[httpie](https://httpie.io/)从命令行向Portainer API发起HTTP调用。您可以使用您偏好的方法替换httpie。

## 准备工作

部署Portainer后，您需要初始化管理员用户。首先初始化管理员密码：

```
http POST https://my-portainer-server:9443/api/users/admin/init Username="admin" Password="adminpassword"
```

现在，使用管理员账户对API进行身份验证。为您的用户名生成授权令牌。此令牌将提供与生成它的用户相同的权限。

```
http POST https://my-portainer-server:9443/api/auth Username="admin" Password="adminpassword"
```

响应是一个包含JWT令牌的JSON对象，令牌位于`jwt`字段中。记下此令牌。在发起API调用时，您将在授权头中使用它。

```
{
  "jwt":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE"
}
```

授权头的值必须采用`Bearer JWT_TOKEN`的形式。使用上面的令牌作为示例，值将如下所示：

```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE
```

JWT令牌在生成后8小时内有效。一旦过期，您需要生成新的令牌。

## 添加环境

### 通过Docker socket添加本地环境 <a href="#local-endpoint-via-the-docker-socket" id="local-endpoint-via-the-docker-socket"></a>

此查询将创建一个名为`test-local`的环境，并将使用Docker socket与您的环境通信。

此示例要求您在运行Portainer时绑定挂载Docker socket。

运行以下命令：

```
http --form POST https://my-portainer-server:9443/api/endpoints \
    "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE" \
    Name="test-local" EndpointCreationType=1
```

响应是一个表示环境的JSON对象：

```
{
    "AuthorizedTeams": [], 
    "AuthorizedUsers": [], 
    "Extensions": [], 
    "GroupId": 1, 
    "Id": 1, 
    "Name": "test-local", 
    "PublicURL": "",
    "Type": 1,
    "TLSConfig": {
        "TLS": false, 
        "TLSSkipVerify": false
    }, 
    "Type": 1, 
    "URL": "unix:///var/run/docker.sock"
}
```

记下`Id`值。它将用于针对端点的Docker Engine执行查询。

### 添加远程环境 <a href="#remote-endpoint" id="remote-endpoint"></a>

此查询将创建一个名为`test-remote`的环境。它将通过TCP与您的环境通信，使用IP地址`10.0.7.10`和端口`2375`。请确保将示例值替换为您自己的IP地址和端口。

Docker API必须在提供的IP地址和端口上公开。要了解如何执行此操作，请参阅Docker文档。

运行以下命令：

```
http --form POST https://my-portainer-server:9443/api/endpoints \
    "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE" \
    Name="test-remote" URL="tcp://10.0.7.10:2375" EndpointCreationType=1
```

响应是一个表示环境的JSON对象：

```
{
    "AuthorizedTeams": [], 
    "AuthorizedUsers": [], 
    "Extensions": [], 
    "GroupId": 1, 
    "Id": 1, 
    "Type": 1,
    "Name": "test-remote", 
    "PublicURL": "", 
    "TLSConfig": {
        "TLS": false, 
        "TLSSkipVerify": false
    }, 
    "Type": 1, 
    "URL": "tcp://10.0.7.10:2375"
}
```

记下`Id`值。它将用于针对环境的Docker Engine执行查询。

### 添加使用TLS的远程环境 <a href="#remote-endpoint-secured-using-tls" id="remote-endpoint-secured-using-tls"></a>

此查询将创建一个名为`test-remote-tls`的环境。它将通过TCP(使用TLS保护)与您的环境通信，使用IP地址`10.0.7.10`和端口`2376`。请确保将示例值替换为您自己的IP地址和端口。

Docker API必须在提供的IP地址和端口上公开。要了解如何执行此操作，请参阅Docker文档。

运行以下命令：

```
http --form POST https://my-portainer-server:9443/api/endpoints \
    "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOjEsImV4cCI6MTQ5OTM3NjE1NH0.NJ6vE8FY1WG6jsRQzfMqeatJ4vh2TWAeeYfDhP71YEE" \
    Name="test-remote-tls" URL="tcp://10.0.7.10:2376" EndpointCreationType=1 TLS="true" TLSCACertFile@/path/to/ca.pem TLSCertFile@/path/to/cert.pem TLSKeyFile@/path/to/key.pem
```

响应是一个表示环境的JSON对象：

```
{
    "AuthorizedTeams": [], 
    "AuthorizedUsers": [], 
    "Extensions": [], 
    "GroupId": 1, 
    "Id": 1, 
    "Type": 1,
    "Name": "test-remote-tls", 
    "PublicURL": "", 
    "TLSConfig": {
        "TLS": true, 
        "TLSCACert": "/data/tls/1/ca.pem", 
        "TLSCert": "/data/tls/1/cert.pem", 
        "TLSKey": "/data/tls/1/key.pem", 
        "TLSSkipVerify": false
    }, 
    "Type": 1, 
    "URL": "tcp://10.0.7.10:2376"
}
```

记下`Id`值。它将用于针对环境的Docker Engine执行查询。
