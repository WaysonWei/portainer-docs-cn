# 将认证和活动日志流式传输到外部提供商

这是一个实验性功能。

从 Portainer 2.20 及更高版本开始，您可以配置将 Portainer 的认证和活动日志以 Syslog 格式流式传输到外部安全信息和事件管理(SIEM)系统。这是通过在启动 Portainer 容器时使用 CLI 标志完成的。

## 可用的 CLI 标志

| 标志                            | 描述                                                                                                                          |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `--syslog-address`              | 流式传输认证和活动日志的 Syslog 地址。仅限 FQDN 或 IP 地址。                                                  |
| `--syslog-port`                 | 上述地址的 Syslog 端口。默认为 `514`。                                                                                |
| `--syslog-protocol`             | 用于向 Syslog 服务器发送日志的协议。支持的值是 `udp`、`tcp` 或 `tcp+tls`。默认为 `udp`。               |
| `--syslog-format`               | 使用的 Syslog 格式。支持的值是 `rfc3164` 或 `rfc5424`。默认为 `rfc5424`。                                        |
| `--syslog-source-hostname`      | 在 Syslog 服务器消息中显示的主机名值。默认为 `portainer`。                                 |
| `--syslog-insecure-skip-verify` | 使用 `tcp+tls` 协议时禁用 TLS 服务器验证。仅应出于测试目的启用。默认为 `false`。              |
| `--syslog-ca-cert`              | Syslog 服务器使用的受信任 CA 的路径。默认为 `/syslog/certs/ca.pem`。                                            |
| `--syslog-cert`                 | 用于通过 mTLS 向 Syslog 服务器进行身份验证的客户端证书路径。默认为 `/syslog/certs/cert.pem`。 |
| `--syslog-key`                  | 用于通过 mTLS 向 Syslog 服务器进行身份验证的客户端密钥路径。默认为 `/syslog/certs/key.pem`。          |

## 使用示例

以下是一个 `docker run` 命令示例，使用上述选项将日志流式传输到 `syslog.mydomain.com` 的 UDP 端口 `514` 上的 SIEM 提供商。

由于这些标志是 Portainer 选项，它们必须在镜像规范之后指定。

```
docker run -d -p 8000:8000 -p 9443:9443 \
    --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ee:lts \
    --syslog-addr=syslog.mydomain.com \
    --syslog-port=514 \
    --syslog-source-hostname="my-portainer-instance"
