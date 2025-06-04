# 在 Portainer 中使用自定义 SSL 证书

默认情况下，Portainer 的 Web 界面和 API 通过安装时生成的自签名证书提供 HTTPS 服务。您可以在安装后[通过 Portainer UI](../admin/settings/#ssl-certificate)替换为您自己的 SSL 证书，或者按照本文说明在安装时进行配置。

使用外部颁发的证书时，请确保通过 `--sslcert` 提供的文件中包含完整的证书链（包括任何中间证书）。否则可能会遇到证书验证问题。您可以从证书颁发机构或[What's My Chain Cert?](https://whatsmychaincert.com/)网站获取证书链。

## 在 Docker Standalone 上使用自定义 SSL 证书

Portainer 需要 PEM 格式的证书。

在安装时使用 `--sslcert` 和 `--sslkey` 标志。

将您的证书（包括证书链）和密钥上传到运行 Portainer 的服务器，然后启动 Portainer 并引用它们。以下命令假设您的证书存储在 `/path/to/your/certs` 目录中，文件名为 `portainer.crt` 和 `portainer.key`，并将该目录绑定挂载到 Portainer 容器中的 `/certs`：

```
docker run -d -p 9443:9443 -p 8000:8000 \
    --name portainer --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -v /path/to/your/certs:/certs \
    portainer/portainer-ee:lts \
    --sslcert /certs/portainer.crt \
    --sslkey /certs/portainer.key
```

```
docker run -d -p 9443:9443 -p 8000:8000 \
    --name portainer --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -v /path/to/your/certs:/certs \
    portainer/portainer-ce:lts \
    --sslcert /certs/portainer.crt \
    --sslkey /certs/portainer.key
```

或者，可以使用 Certbot 生成证书和密钥。由于 Docker 对符号链接有问题，如果使用 Certbot，您需要将 'live' 和 'archive' 目录都作为卷挂载，并使用完整链证书。例如：

```
docker run -d -p 9443:9443 -p 8000:8000 \
    --name portainer --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -v /etc/letsencrypt/live/yourdomain:/certs/live/yourdomain:ro \
    -v /etc/letsencrypt/archive/yourdomain:/certs/archive/yourdomain:ro \
    portainer/portainer-ee:lts \
    --sslcert /certs/live/yourdomain/fullchain.pem \
    --sslkey /certs/live/yourdomain/privkey.pem
```

```
docker run -d -p 9443:9443 -p 8000:8000 \
    --name portainer --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -v /etc/letsencrypt/live/yourdomain:/certs/live/yourdomain:ro \
    -v /etc/letsencrypt/archive/yourdomain:/certs/archive/yourdomain:ro \
    portainer/portainer-ce:lts \
    --sslcert /certs/live/yourdomain/fullchain.pem \
    --sslkey /certs/live/yourdomain/privkey.pem
```

完成后，您可以访问 `https://$ip-docker-host:9443`。

## 在 Docker Swarm 上使用自定义 SSL 证书

要为 Docker Swarm 提供自定义 SSL 证书，只需定义 `portainer.sslcert` 和 `portainer.sslkey` 密钥，安装清单将自动检测并使用它们：

```
docker secret create portainer.sslcert /path/to/your/certificate.crt
docker secret create portainer.sslkey /path/to/your/certificate.key
```

接下来，获取堆栈 YML 清单：

**商业版：**
```
curl -L https://downloads.portainer.io/ee-lts/portainer-agent-stack-ssl.yml -o portainer-agent-stack.yml
```

**社区版：**
```
curl -L https://downloads.portainer.io/ce-lts/portainer-agent-stack-ssl.yml -o portainer-agent-stack.yml
```

**商业版(Windows)：**
```
curl https://downloads.portainer.io/ee-lts/portainer-windows-stack-ssl.yml -o portainer-agent-stack.yml
```

**社区版(Windows)：**
```
curl https://downloads.portainer.io/ce-lts/portainer-windows-stack-ssl.yml -o portainer-agent-stack.yml
```

最后，使用下载的 YML 清单部署您的堆栈：
```
docker stack deploy -c portainer-agent-stack.yml portainer
```

有关密钥的更多信息，请阅读[Docker 官方文档](https://docs.docker.com/compose/compose-file/#secrets)。

## 在 Kubernetes 上使用自定义 SSL 证书(通过 Helm)

如果不存在，请先创建 `portainer` 命名空间：
```
kubectl create namespace portainer
```

接下来，创建一个包含完整证书链和匹配私钥的 TLS 密钥：
```
kubectl create secret tls portainer-tls-secret -n portainer \
    --cert=/path/to/cert/file \
    --key=/path/to/key/file
```

通过 helm 安装，并将 `tls.existingSecret` 参数设置为您刚创建的密钥名称：

**商业版：**
```
helm install -n portainer portainer portainer/portainer \
    --set tls.existingSecret=portainer-tls-secret \
    --set enterpriseEdition.enabled=true
```

**社区版：**
```
helm install -n portainer portainer portainer/portainer \
    --set tls.existingSecret=portainer-tls-secret
```

**商业版(LoadBalancer)：**
```
helm install -n portainer portainer portainer/portainer \
    --set tls.existingSecret=portainer-tls-secret \
    --set service.type=LoadBalancer \
    --set enterpriseEdition.enabled=true 
```

**社区版(LoadBalancer)：**
```
helm install -n portainer portainer portainer/portainer \
    --set tls.existingSecret=portainer-tls-secret \
    --set service.type=LoadBalancer
