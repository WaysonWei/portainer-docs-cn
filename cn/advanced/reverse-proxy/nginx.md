# 在 nginx 反向代理后部署 Portainer

## 在 Docker Standalone 场景中部署

要在 Docker standalone 场景中将 Portainer 部署在 nginx 代理后面，您必须使用 Docker Compose 文件。在下面的 docker-compose.yml 中，您将找到 nginx 代理和 Portainer Server 的配置。

此示例使用优秀的 [nginxproxy/nginx-proxy](https://hub.docker.com/r/nginxproxy/nginx-proxy) 镜像作为代理容器，除了添加到 `portainer` 容器定义中的两个环境变量外，不需要额外的配置。

```
version: "2"

services:
  nginx-proxy:
    image: nginxproxy/nginx-proxy
    restart: always
    ports:
      - "80:80"
    volumes:
      - "/var/run/docker.sock:/tmp/docker.sock:ro"

  portainer:
    image: portainer/portainer-ee:lts
    command: -H unix:///var/run/docker.sock
    restart: always
    environment:
      - VIRTUAL_HOST=portainer.yourdomain.com
      - VIRTUAL_PORT=9000
    ports:
      - 8000:8000
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:
```

```
version: "2"

services:
  nginx-proxy:
    image: nginxproxy/nginx-proxy
    restart: always
    ports:
      - "80:80"
    volumes:
      - "/var/run/docker.sock:/tmp/docker.sock:ro"

  portainer:
    image: portainer/portainer-ce:lts
    command: -H unix:///var/run/docker.sock
    restart: always
    environment:
      - VIRTUAL_HOST=portainer.yourdomain.com
      - VIRTUAL_PORT=9000
    ports:
      - 8000:8000
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:
```

要开始使用此配置，请更改 `VIRTUAL_HOST` 值，然后运行以下命令部署 Portainer：

```
docker-compose up -d
```

完成后，运行 `docker ps`。您应该看到类似以下的输出：

```
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                                                           NAMES
8c8f2eac7c9a   portainer/portainer-ee:lts      "/portainer -H unix:…"   4 minutes ago   Up 4 minutes   9000/tcp, 0.0.0.0:8000->8000/tcp, :::8000->8000/tcp, 9443/tcp   portainer_portainer_1
3e7c8b5d71d7   nginxproxy/nginx-proxy          "/app/docker-entrypo…"   4 minutes ago   Up 4 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp                               portainer_nginx-proxy_1
```

部署完成后，您可以访问 `portainer.yourdomain.com`。

## 在 Docker Swarm 场景中部署

在 Docker Swarm 中将 Portainer 部署在 nginx 后面与 Docker Standalone 场景有相似的步骤。在部署之前，您需要创建两个元素：网络和卷。

此部署假设您正在运行一个管理节点。如果您使用多个管理节点，我们建议在继续之前[阅读此知识库文章](https://portal.portainer.io/knowledge/how-can-i-ensure-portainers-configuration-is-retained)。

首先，创建两个网络：

* 一个用于 agent 和与 Portainer Server 的通信
* 一个用于将 Portainer 容器"暴露"到与反向代理相同的网络

```
docker network create -d overlay proxy
```

```
docker network create -d overlay agent_network
```

接下来，创建卷：

```
docker volume create portainer_data
```

最后，将以下配置保存为 `portainer.yml`：

```
version: '3.2'

services:
  nginx-proxy:
    image: nginxproxy/nginx-proxy
    networks:
      - proxy
    ports:
      - "80:80"
    volumes:
      - "/var/run/docker.sock:/tmp/docker.sock:ro"
      - "./vhost.d:/etc/nginx/vhost.d:ro"

  agent:
    image: portainer/agent:lts
    environment:
      # 必需：在覆盖网络内部署时应等于服务名称前缀为"tasks."
      AGENT_CLUSTER_ADDR: tasks.agent
      # AGENT_PORT: 9001
      # LOG_LEVEL: DEBUG
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes:/var/lib/docker/volumes
    networks:
      - agent_network
    deploy:
      mode: global
      placement:
        constraints: [node.platform.os == linux]

  portainer:
    image: portainer/portainer-ee:lts
    command: -H tcp://tasks.agent:9001 --tlsskipverify
    volumes:
      - data:/data
    environment:
      - VIRTUAL_HOST=portainer.yourdomain.com
      - VIRTUAL_PORT=9000
    ports:
      - 8000:8000
    networks:
      - proxy
      - agent_network
    deploy:
      mode: replicated
      replicas: 1
      placement:
        constraints: [node.role == manager]

networks:
  proxy:
    external: true
  agent_network:
    external: true

volumes:
   data:
```

```
version: '3.2'

services:
  nginx-proxy:
    image: nginxproxy/nginx-proxy
    networks:
      - proxy
    ports:
      - "80:80"
    volumes:
      - "/var/run/docker.sock:/tmp/docker.sock:ro"
      - "./vhost.d:/etc/nginx/vhost.d:ro"

  agent:
    image: portainer/agent:lts
    environment:
      # 必需：在覆盖网络内部署时应等于服务名称前缀为"tasks."
      AGENT_CLUSTER_ADDR: tasks.agent
      # AGENT_PORT: 9001
      # LOG_LEVEL: DEBUG
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes:/var/lib/docker/volumes
    networks:
      - agent_network
    deploy:
      mode: global
      placement:
        constraints: [node.platform.os == linux]

  portainer:
    image: portainer/portainer-ce:lts
    command: -H tcp://tasks.agent:9001 --tlsskipverify
    volumes:
      - data:/data
    environment:
      - VIRTUAL_HOST=portainer.yourdomain.com
      - VIRTUAL_PORT=9000
    ports:
      - 8000:8000
    networks:
      - proxy
      - agent_network
    deploy:
      mode: replicated
      replicas: 1
      placement:
        constraints: [node.role == manager]

networks:
  proxy:
    external: true
  agent_network:
    external: true

volumes:
   data:
```

要开始使用此配置，请更改 `VIRTUAL_HOST` 值，然后运行以下命令部署 Portainer：

```
docker stack deploy portainer -c portainer.yml
```

要检查部署情况，请运行 `docker service ls`。您应该看到类似以下的输出：

```
ID                  NAME                    MODE                REPLICAS            IMAGE                          PORTS
gy2bjxid0g4p        portainer_agent         global              1/1                 portainer/agent:lts
jwvjp5bux4sz        portainer_nginx-proxy   replicated          1/1                 nginxproxy/nginx-proxy:latest  *:80->80/tcp
5nflcvoxl3c7        portainer_portainer     replicated          1/1                 portainer/portainer-ee:lts     *:8000->8000/tcp
```

一旦服务运行，您将能够从您之前定义的 URL 访问 Portainer，例如：`portainer.yourdomain.com`。
