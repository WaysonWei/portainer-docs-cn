# CLI 配置选项

## 命令行可用的配置标志

| 标志                                                   | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--admin-password`                                     | 指定管理员用户的bcrypt哈希密码。这只能在首次创建管理员用户时使用（例如在安装期间），不能用于安装后更改管理员用户密码。                                                                                                                                                                                                                                |
| `--admin-password-file`                                | 指定包含管理员用户密码的文件路径。这只能在首次创建管理员用户时使用（例如在安装期间），不能用于安装后更改管理员用户密码。                                                                                                                                                                                                            |
| `--base-url`                                           | <p>指定Portainer运行的基础路径，如果您在反向代理后的子路径中运行Portainer（例如，如果您在<code>https://yourdomain/portainer</code>运行Portainer，则使用<code>--base-url /portainer</code>）。默认为<code>/</code>。<br><strong>注意：</strong>使用此选项时，您仍需要确保反向代理配置会剥离指定的子路径。</p> |
| <p><code>--bind</code></p><p><code>-p</code></p>       | 指定提供Portainer服务的地址和端口（默认：`:9000`）。                                                                                                                                                                                                                                                                                                                                                             |
| `--bind-https`                                         | 指定通过HTTPS提供Portainer服务的地址和端口（默认：`:9443`）。                                                                                                                                                                                                                                                                                                                                                   |
| <p><code>--data</code></p><p><code>-d</code></p>       | 指定Portainer数据存储的目录（Linux上默认为`/data`，Windows上默认为`C:\data`）。                                                                                                                                                                                                                                                                                                                                |
| `--edge-compute`                                       | 自动启用边缘计算功能。                                                                                                                                                                                                                                                                                                                                                                                                 |
| <p><code>--hide-label</code></p><p><code>-l</code></p> | 在UI中隐藏带有特定标签的容器。                                                                                                                                                                                                                                                                                                                                                                                            |
| `--http-disabled`                                      | 仅在HTTPS上提供Portainer服务。覆盖`--http-enabled`。在启用此选项前，请确保您的HTTPS配置完全正常工作，并且任何Agent都配置为使用HTTPS。                                                                                                                                                                                                                                                                    |
| `--http-enabled`                                       | 在HTTP上提供Portainer服务。如果与`--http-disabled`一起使用，则忽略此选项。                                                                                                                                                                                                                                                                                                                                                     |
| <p><code>--host</code></p><p><code>-H</code></p>       | 指定Docker守护程序端点。                                                                                                                                                                                                                                                                                                                                                                                                        |
| `--license-key`                                        | 指定要使用的许可证密钥。仅适用于Portainer商业版。                                                                                                                                                                                                                                                                                                                                                             |
| `--log-level`                                          | 设置Portainer应用程序的日志级别，例如`--log-level DEBUG`。这在故障排除时很有用。也可以通过[设置](../admin/settings/)启用调试日志记录。                                                                                                                                                                                                                                              |
| `--log-mode`                                           | 设置Portainer日志输出的格式，例如`--log-mode NOCOLOR`。选项有：`PRETTY`（默认）、`NOCOLOR`（禁用颜色代码）、`JSON`（JSON格式的日志）。                                                                                                                                                                                                                                                          |
| `--logo`                                               | 指定要在UI中显示为徽标的图像的URL。如果未指定，则使用Portainer徽标。                                                                                                                                                                                                                                                                                                                    |
| `--mtlscacert`                                         | 指定用于mTLS通信的证书颁发机构(CA)证书的路径。（仅限商业版）                                                                                                                                                                                                                                                                                                                                      |
| `--mtlscert`                                           | 指定用于mTLS通信的证书的路径。（仅限商业版）                                                                                                                                                                                                                                                                                                                                                                 |
| `--mtlskey`                                            | 指定用于mTLS通信的证书密钥的路径。（仅限商业版）                                                                                                                                                                                                                                                                                                                                                             |
| `--snapshot-interval`                                  | 指定两个环境快照作业之间的时间间隔，以字符串表示。例如30s、5m、1h...支持`time.ParseDuration`方法（默认：5m）。                                                                                                                                                                                                                                                                |
| `--sslcacert`                                          | 指定用于验证Edge Agent证书的证书颁发机构(CA)证书的路径。（仅限商业版，**已弃用**，请改用[mTLS](mtls.md)）                                                                                                                                                                                                                                                                         |
| `--sslcert`                                            | 指定用于保护Portainer实例的SSL证书的路径（Linux上默认为`/certs/portainer.crt`，Windows上默认为`C:\certs\portainer.crt`）。                                                                                                                                                                                                                                                                             |
| `--sslkey`                                             | 指定用于保护Portainer实例的SSL密钥的路径（Linux上默认为`/certs/portainer.key`，Windows上默认为`C:\certs\portainer.key`）。                                                                                                                                                                                                                                                                                     |
| `--syslog-*`                                           | `--syslog-*`选项用于配置将认证和活动日志流式传输到外部Syslog兼容提供程序。有关此实验性功能的更多信息，请参阅[SIEM文档](siem.md)。                                                                                                                                                                                                                                       |
| <p><code>--templates</code></p><p><code>-t</code></p>  | 指定模板（应用程序）定义的URL。                                                                                                                                                                                                                                                                                                                                                                                       |
| `--tlscacert`                                          | 指定用于Docker守护程序连接的CA的路径（Linux上默认为`/certs/ca.pem`，Windows上默认为`C:\certs\ca.pem`）。                                                                                                                                                                                                                                                                                                           |
| `--tlscert`                                            | 指定用于Docker守护程序连接的TLS证书文件的路径（Linux上默认为`/certs/cert.pem`，Windows上默认为`C:\certs\cert.pem`）。                                                                                                                                                                                                                                                                                              |
| `--tlskey`                                             | 指定用于Docker守护程序连接的TLS密钥的路径（Linux上默认为`/certs/key.pem`，Windows上默认为`C:\certs\key.pem`）。                                                                                                                                                                                                                                                                                                             |
| `--tlsverify`                                          | TLS支持（默认：`false`）。                                                                                                                                                                                                                                                                                                                                                                                                              |
| `--tlsskipverify`                                      | 禁用TLS服务器验证。                                                                                                                                                                                                                                                                                                                                                                                                             |
| `--tunnel-addr`                                        | 指定用于Edge Agent的隧道监听地址。默认为`0.0.0.0`（所有接口）。                                                                                                                                                                                                                                                                                                                               |
| `--tunnel-port`                                        | 指定与Edge Agent一起使用的备用隧道端口。使用`--tunnel-port 8001`和`-p 8001:8001`使Edge Agent在端口`8001`上通信。                                                                                                                                                                                                                                                                               |
| `--version`                                            | 显示Portainer的版本。                                                                                                                                                                                                                                                                                                                                                                                                            |

## 创建管理员账户和密码

本节中的命令将自动创建一个名为`admin`的管理员账户，并指定密码。这只能在首次创建管理员用户时使用（例如在安装期间），不能用于安装后更改管理员用户密码。

### 方法1：从命令行创建账户

您可以从命令行为管理员账户指定bcrypt加密的密码。如果已安装`apache2-utils`包，请使用以下命令创建密码：

```
htpasswd -nb -B admin "your-password" | cut -d ":" -f 2
```

如果您的系统没有该命令，请使用容器运行该命令：

```
docker run --rm httpd:2.4-alpine htpasswd -nbB admin "your-password" | cut -d ":" -f 2
```

创建密码后，通过使用`--admin-password`标志启动Portainer从命令行指定管理员密码：

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ee:lts --admin-password='$2y$05$8oz75U8m5tI/xT4P0NbSHeE7WyRzOWKRBprfGotwDkhBOGP/u802u'
```

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce:lts --admin-password='$2y$05$8oz75U8m5tI/xT4P0NbSHeE7WyRzOWKRBprfGotwDkhBOGP/u802u'
```

### 方法2：使用文件创建账户

您还可以将纯文本密码存储在文件中并使用`--admin-password-file`标志。首先，使用以下示例命令将密码添加到文件中：

```
echo -n mypassword > /tmp/portainer_password
```

接下来，启动Portainer容器：

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock -v /tmp/portainer_password:/tmp/portainer_password portainer/portainer-ee:lts --admin-password-file /tmp/portainer_password
```

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock -v /tmp/portainer_password:/tmp/portainer_password portainer/portainer-ce:lts --admin-password-file /tmp/portainer_password
```

这也适用于Docker Swarm和Docker Secrets：

```
echo -n mypassword | docker secret create portainer-pass -
```

```
docker service create \
    --name portainer \
    --secret portainer-pass \
    --publish 9443:9443 \
    --publish 8000:8000 \
    --replicas=1 \
    --constraint 'node.role == manager' \
    --mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
    portainer/portainer-ee:lts \
    --admin-password-file '/run/secrets/portainer-pass' \
    -H unix:///var/run/docker.sock
```

```
docker service create \
    --name portainer \
    --secret portainer-pass \
    --publish 9443:9443 \
    --publish 8000:8000 \
    --replicas=1 \
    --constraint 'node.role == manager' \
    --mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
    portainer/portainer-ce:lts \
    --admin-password-file '/run/secrets/portainer-pass' \
    -H unix:///var/run/docker.sock
```

## 隐藏特定容器

Portainer允许您使用`-l`标志隐藏带有特定标签的容器。以下是一个带有`owner=acme`标签的容器示例：

```
docker run -d --label owner=acme nginx
```

要隐藏此容器，在启动Portainer时在CLI上添加`-l owner=acme`选项：

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ee:lts -l owner=acme
```

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce:lts -l owner=acme
```

要隐藏多个容器，重复`-l`标志：

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ee:lts -l owner=acme -l service=secret
```

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce:lts -l owner=acme -l service=secret
```

## 使用您自己的徽标

图像大小必须恰好为155px × 55px。

使用`--logo`标志指定图像文件的位置，替换我们的徽标：

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ee:lts --logo "https://www.docker.com/sites/all/themes/docker/assets/images/brand-full.svg"
```

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce:lts --logo "https://www.docker.com/sites/all/themes/docker/assets/images/brand-full.svg"
```

您还可以在Portainer UI（**设置**菜单）中更新徽标。

## 定义您自己的应用模板

我们建议在[GitHub](https://www.github.com/)上托管模板文件，以便Portainer无需身份验证即可访问它们。

Portainer允许您快速[使用应用模板部署容器](../user/docker/templates/deploy-container.md)。默认情况下，将使用Portainer模板，但您也可以定义自己的模板。

模板仅在Portainer首次启动时加载一次。如果您已经部署了Portainer实例然后决定使用自己的模板，您需要通过用户界面或HTTP API清除默认模板。使用`--templates`标志指定可以通过HTTP访问模板文件的URL。

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ee:lts --templates http://my-host.my-domain/templates.json
```

```
docker run -d -p 9443:9443 -p 8000:8000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer-ce:lts --templates http://my-host.my-domain/templates.json
