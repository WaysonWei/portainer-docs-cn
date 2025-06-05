# 访问 Portainer API

要访问 Portainer API，您需要准备以下内容：

* Portainer 中的用户账号
* 该用户的访问令牌
* 能够向 Portainer 服务器发送 HTTPS 请求（端口为 `9443`，旧版 HTTP 使用 `9000` 端口）

## 创建新用户

API 访问是按用户授权的，每个用户的 API 访问权限取决于该用户在 Portainer 中的权限设置。例如，如果您的用户只能访问一个环境，那么该用户的 API 调用也将仅限于该环境。

要在 Portainer 中创建新用户，请参考我们的文档：

[add.md](../admin/user/add.md)

用户创建完成后，请以该用户身份登录 Portainer 以创建 API 访问令牌。

## 创建访问令牌

用户创建完成后，您可以为该用户添加访问令牌。访问令牌将提供与该用户通过 Portainer UI 登录相同的功能访问级别。

以该用户身份登录后，点击右上角的用户名，然后选择**我的账户**。

<figure><img src="/assets/2.20-api-access-myaccount.gif" alt=""><figcaption></figcaption></figure>

向下滚动到**访问令牌**部分。在这里您可以看到该用户现有的所有访问令牌。

<figure><img src="/assets/2.15-accountsettings-apitokens.png" alt=""><figcaption></figcaption></figure>

要添加新的访问令牌，请点击**添加访问令牌**按钮。您将被引导至一个新页面，可以在此为访问令牌设置**描述**。我们建议将其设置为易于识别的名称以便日后参考。

出于安全考虑，创建访问令牌时需要重新输入密码。

<figure><img src="/assets/2.20-api-access-createtoken.png" alt=""><figcaption></figcaption></figure>

提供描述后，点击**添加访问令牌**按钮生成您的访问令牌。

您的新访问令牌现在将显示出来。请复制访问令牌并妥善保存，因为创建后将无法再次查看该令牌。

<figure><img src="/assets/2.20-api-access-createdtoken.png" alt=""><figcaption></figcaption></figure>

复制访问令牌后，点击**完成**按钮返回用户设置页面。您的访问令牌现在可以使用了。

## 使用访问令牌

现在您已经创建了用户和访问令牌，可以开始访问 API 了。Portainer API 遵循 RESTful 架构，接受 `GET`/`POST`/`PUT`/`DELETE` 请求并以 JSON 对象响应。

以下示例使用 [httpie](https://httpie.org/) 执行针对 Portainer 的 API 调用。您可以根据需要替换为其他方法。

要发起 API 请求，您需要在 `X-API-Key` 头中包含访问令牌以验证请求。例如，您可以使用 `/stacks` 端点列出您有权访问的堆栈：

```
http GET https://portainer-url:9443/api/stacks X-API-Key:your_api_key_here
```

这将返回一个列出您的堆栈的 JSON 对象：

```
[
    {
        "AdditionalFiles": null,
        "AutoUpdate": null,
        "CreatedBy": "admin",
        "CreationDate": 1631852794,
        "EndpointId": 4,
        "EntryPoint": "docker-compose.yml",
        "Env": null,
        "GitConfig": {
            "Authentication": null,
            "ConfigFilePath": "docker-compose.yml",
            "ConfigHash": "2e71920bf1ee1bbac976d320f8f274411fba3bad",
            "ReferenceName": "refs/heads/master",
            "URL": "https://github.com/mygithubaccount/wordpress-stack"
        },
        "Id": 5,
        "IsComposeFormat": true,
        "Name": "",
        "Namespace": "my-namespace",
        "ProjectPath": "/data/compose/5",
        "ResourceControl": null,
        "Status": 1,
        "SwarmId": "",
        "Type": 3,
        "UpdateDate": 0,
        "UpdatedBy": ""
    },
]
```

如果用户尝试访问没有权限的区域，将返回错误信息。例如，假设一个非管理员用户尝试访问需要管理员权限的 `/settings` 端点：

```
http GET https://portainer:9443/api/settings X-API-Key:your_api_key_here
```

用户将收到以下响应：

```
{
    "details": "Unauthorized",
    "message": "Access denied"
}
```

现在您已经可以访问 Portainer API，可以从 [API 文档](docs.md) 和我们的 [使用示例](examples.md) 中了解更多使用方法。
