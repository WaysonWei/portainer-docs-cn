# 在 Portainer 中使用 mTLS

双向 TLS（或 **mTLS**）是一种基于证书的系统，客户端和服务器（在本例中为 Portainer Edge Agent 和 Portainer Server）通过受信任的源（证书颁发机构）相互进行加密身份验证。这可以作为额外的安全层来保护 Edge Agent 和 Portainer 之间的通信。在此设置下，如果第三方系统尝试与 Portainer Server 通信但未使用由证书颁发机构签名的证书，则将被拒绝。

本文将引导您完成部署支持 mTLS 的 Portainer Server 和 Edge Agents 的过程。

mTLS 支持仅在 Portainer 商业版中可用。

## 要求

要为 Portainer 配置 mTLS 支持，您需要以下内容：

* Portainer Server 和 Portainer Edge Agent
* 证书颁发机构 (CA)。您可以使用自己的企业 CA 或完全控制证书颁发策略的 CA
* CA 证书，PEM 格式 (`mtlsca.crt`)
* 可以指向 Portainer Server 实例以专门用于 mTLS 的域（或子域）。这将是服务器证书颁发的域
* 由您的 CA 为 Portainer Server 颁发的服务器证书 (`mtlsserver.crt`) 和相应的密钥 (`mtlsserver.key`)，PEM 格式。确保这些证书在 `extendedKeyUsage` 中选择了 `serverAuth`。此证书应将用于 mTLS 的域（或子域）作为主题备用名称 (SAN)
* 由您的 CA 为 Edge Agent 颁发的客户端证书 (`client.crt`) 和相应的密钥 (`client.key`)，PEM 格式。确保这些证书在 `extendedKeyUsage` 中选择了 `clientAuth`

## 配置 Portainer Server

要与 Edge Agents 一起使用 mTLS，必须为 Portainer Server 实例配置 mTLS 支持。这可以在 Portainer Server 实例的初始安装期间完成，也可以在安装后通过 [Edge Compute 设置](../admin/settings/edge.md#mtls-certificate) 完成。

### 在安装期间配置 mTLS

部署 Portainer Server 时，您需要使 CA 证书、服务器证书和服务器密钥对 Portainer 可用。具体操作取决于您的部署方式。

#### Docker Standalone

在 Docker 主机上，将您的 CA 证书 (`mtlsca.crt`)、服务器证书 (`mtlsserver.crt`) 和服务器密钥 (`mtlsserver.key`) 上传到将绑定挂载到 Portainer 容器的目录中。在此示例中，我们假设您的证书位于 `/root/certs`。

修改您的 `docker run` 命令以将 `/root/certs` 目录挂载到 `/certs` 并添加 `--mtlscacert`、`--mtlscert` 和 `--mtlskey` 选项：

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always \ 
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -v /root/certs:/certs \
    portainer/portainer-ee:lts \
    --mtlscacert /certs/mtlsca.crt \    
    --mtlscert /certs/mtlsserver.crt \
    --mtlskey /certs/mtlsserver.key
```

这将使用您提供的 CA 和证书启动 Portainer。

#### Docker Swarm

要在安装期间将 mTLS 证书添加到 Docker Swarm 上的 Portainer Server，我们建议将必要的文件添加为 secret，然后在用于部署 Portainer 的 YAML 中引用这些 secret。

首先，将您的 CA 证书 (`mtlsca.crt`)、服务器证书 (`mtlsserver.crt`) 和服务器密钥 (`mtlsserver.key`) 上传到将由 secret 创建引用的目录中。在此示例中，我们假设您的证书位于 `/root/certs`。上传文件后，按如下方式创建您的 secret：

```
docker secret create portainer.mtlscacert /root/certs/mtlsca.crt
docker secret create portainer.mtlscert /root/certs/mtlsserver.crt
docker secret create portainer.mtlskey /root/certs/mtlsserver.key
```

修改您的 Portainer YAML 文件以附加 secret 并添加 `--mtlscacert`、`--mtlscert` 和 `--mtlskey` 选项：

```yaml
  portainer:
    image: portainer/portainer-ee:lts
    command: -H tcp://tasks.agent:9001 --tlsskipverify --mtlscacert /run/secrets/portainer.mtlscacert --mtlscert /run/secrets/portainer.mtlscert --mtlskey /run/secrets/portainer.mtlskey
    ports:
      - "9443:9443"
      - "9000:9000"
      - "8000:8000"
    volumes:
      - portainer_data:/data
    networks:
      - agent_network
    deploy:
      mode: replicated
      replicas: 1
      placement:
        constraints: [node.role == manager]
    secrets:
        - portainer.mtlscacert
        - portainer.mtlsscert
        - portainer.mtlskey
```

并添加 `secrets` 定义以包含我们刚刚创建的 secret：

```yaml
secrets:
  portainer.mtlscacert:
    external: true
  portainer.mtlscert:
    external: true
  portainer.mtlskey:
    external: true
```

#### Kubernetes (通过 Helm)

如果尚不存在，请创建 `portainer` 命名空间：

```
kubectl create namespace portainer
```

接下来，创建一个包含 CA、证书和匹配私钥的 secret：

```
kubectl create secret generic portainer-mtls-certs-secret -n portainer \
    --from-file=mtlsca.crt=ca.crt \
    --from-file=mtlscert.crt=server.crt \
    --from-file=mtlskey.key=server.key
```

将上述命令中的 `ca.crt`、`server.crt` 和 `server.key` 替换为您的 CA 证书、证书和匹配密钥的路径。

通过 Helm 安装 Portainer，并将 `mtls.existingSecret` 参数设置为您刚刚创建的 secret 的名称：

```
helm install -n portainer portainer portainer/portainer \
    --set mtls.existingSecret=portainer-mtls-certs-secret \
    --set enterpriseEdition.enabled=true
```

### 安装后配置 mTLS

如果您已经部署了 Portainer Server，则可以通过 Portainer UI 配置 mTLS 支持。

作为管理员用户，从左菜单中选择 **Settings**，然后选择 **Edge Compute**。如果尚未启用，请切换 **Enable Edge Compute features** 并点击 **Save Settings**。然后向下滚动到 **mTLS Certificate** 部分。

<figure><img src="/assets/2.18-settings-edge-mtls.png" alt=""><figcaption></figcaption></figure>

在这里，您可以使用 **Use separate mTLS cert** 切换启用 mTLS，并使用 **TLS CA certificate**、**TLS certificate** 和 **TLS key** 按钮分别上传 CA 证书、服务器证书和服务器密钥。

如果通过此方法添加或更改 mTLS CA 证书，则需要重新启动 Portainer Server 才能使更改生效。您还应确保使用 mTLS 的任何 Edge Agents 也更新为使用新的 CA 证书。

## 部署 Edge Agents

将 Portainer Server 实例配置为使用 mTLS 后，您就可以配置 Edge Agent 部署以使用它。

部署 Edge Agent 时，Portainer UI 将为您提供要运行的命令。我们将获取该命令并修改它以支持 mTLS。

### Docker Standalone

在 Docker 主机上，将您的 CA 证书 (`mtlsca.crt`)、客户端证书 (`client.crt`) 和客户端密钥 (`client.key`) 上传到将绑定挂载到 Edge Agent 容器的目录中。在此示例中，我们假设您的证书位于 `/root/certs`。

证书就位并创建 secret 后，您就可以开始在 Portainer UI 中设置 Edge Agent。

执行此操作时，请记住将您为 mTLS 使用选择的域（或子域）（以及服务器证书颁发的域）用作 Portainer API 服务器 URL 和隧道地址（如果适用）。

在 Portainer UI 中完成 Edge Agent 设置并获得部署命令后，修改命令以将 `/root/certs` 目录挂载到 `/certs`，将 `EDGE_INSECURE_POLL` 选项更改为 `0`，并添加 `--mtlscacert`、`--mtlscert` 和 `--mtlskey` 选项：

```bash
docker run -d \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /var/lib/docker/volumes:/var/lib/docker/volumes \
  -v /:/host \
  -v /root/certs:/certs \
  -v portainer_agent_data:/data \
  --restart always \
  -e EDGE=1 \
  -e EDGE_ID=your-edge-id \
  -e EDGE_KEY=your-edge-key \
  -e EDGE_INSECURE_POLL=0 \
  --name portainer_edge_agent \
  portainer/agent:lts \
  --mtlscacert /certs/mtlsca.crt \
  --mtlscert /certs/client.crt \
  --mtlskey /certs/client.key
```

运行命令以部署支持 mTLS 的 Edge Agent。

### Docker Swarm

要将 mTLS 证书添加到 Edge Agent，我们建议将必要的文件添加为 secret，然后在用于部署 Portainer 的 YAML 中引用这些 secret。

首先，将您的 CA 证书 (`mtlsca.crt`)、客户端证书 (`client.crt`) 和客户端密钥 (`client.key`) 上传到将由 secret 创建引用的目录中。在此示例中，我们假设您的证书位于 `/root/certs`。上传文件后，按如下方式创建您的 secret：

```
docker secret create portainer.mtlscacert /root/certs/mtlsca.crt
docker secret create portainer.mtlscert /root/certs/client.crt
docker secret create portainer.mtlskey /root/certs/client.key
```

证书就位并创建 secret 后，您就可以开始在 Portainer UI 中设置 Edge Agent。

执行此操作时，请记住将您为 mTLS 使用选择的域（或子域）（以及服务器证书颁发的域）用作 Portainer API 服务器 URL 和隧道地址（如果适用）。

在 Portainer UI 中完成 Edge Agent 设置并获得部署命令后，修改命令以将 `EDGE_INSECURE_POLL` 选项更改为 `0` 并添加 `--mtlscacert`、`--mtlscert` 和 `--mtlskey` 选项，使用我们上面定义的 secret：

```bash
docker network create \
  --driver overlay \
  portainer_agent_network;

docker service create \
  --name portainer_edge_agent \
  --network portainer_agent_network \
  -e EDGE=1 \
  -e EDGE_ID=your-edge-id \
  -e EDGE_KEY=your-edge-key \
  -e EDGE_INSECURE_POLL=0 \
  -e AGENT_CLUSTER_ADDR=tasks.portainer_edge_agent \
  --mode global \
  --constraint 'node.platform.os == linux' \
  --mount type=bind,src=//var/run/docker.sock,dst=/var/run/docker.sock \
  --mount type=bind,src=//var/lib/docker/volumes,dst=/var/lib/docker/volumes \
  --mount type=bind,src=//,dst=/host \
  --mount type=volume,src=portainer_agent_data,dst=/data \
  portainer/agent:lts \
  --mtlscacert /run/secrets/portainer.mtlscacert \
  --mtlscert /run/secrets/portainer.mtlscert \
  --mtlskey /run/secrets/portainer.mtlskey
```

运行命令以部署支持 mTLS 的 Edge Agent。

### Kubernetes

目前，Kubernetes 环境上运行的 Portainer Agent 的 mTLS 支持正在开发中。如果您需要在 Kubernetes 环境上部署支持 mTLS 的 Portainer Agent 的说明，请 [联系我们的支持团队](../#getting-support)。
