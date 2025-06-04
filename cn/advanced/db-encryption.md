# 加密Portainer数据库

Portainer使用BoltDB数据库存储配置，该数据库保存在安装期间创建的`portainer_data`卷中。可以通过在启动Portainer Server时提供密钥来加密此数据库以增强安全性。可以在初始安装期间或之后添加加密。

目前，数据库加密是不可逆的。

## Docker Standalone

要在Docker Standalone上启用加密，首先需要创建一个密钥，然后修改docker run命令以将密钥挂载到容器中。

### 创建密钥

在运行Docker Standalone的系统上创建一个文本文件，该文件对Docker可执行文件可访问但又安全。在此示例中，我们假设文件名为`/root/secrets/portainer`。在此文件中输入一个密钥。这将是用于加密Portainer数据库的密钥。

### 挂载密钥

如果Portainer已在运行，您需要先停止并删除Portainer容器：

```
docker stop portainer
docker rm portainer
```

要加密数据库，在`docker run`命令中添加一个绑定挂载，将您的密钥挂载到`/run/secrets/portainer`：

```
-v /root/secrets/portainer:/run/secrets/portainer
```

您最终的`docker run`命令可能如下所示：

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -v /root/secrets/portainer:/run/secrets/portainer \
    portainer/portainer-ee:lts
```

当Portainer容器启动时，它将加密任何现有数据库，或者对于全新安装，将在安装过程中创建一个新的加密数据库。

## Docker Swarm

要在Docker Swarm上启用加密，首先需要创建一个密钥。然后要么更新服务以包含新密钥（如果您有现有的Portainer安装），要么编辑用于创建堆栈的compose文件以包含密钥（如果这是Portainer的全新安装）。

### 创建密钥

在管理节点上，可以运行以下命令创建密钥：

```
echo "这是一个密钥" | docker secret create portainer -
```

将`这是一个密钥`替换为您的密钥。这将创建一个名为`portainer`的密钥，该密钥将用于加密Portainer数据库。

您也可以在Portainer中创建密钥，如果您要向现有安装添加加密。

### 现有安装：更新服务

要向Docker Swarm上的现有Portainer部署添加加密，可以在管理节点上使用以下命令：

```
docker service update \
    --secret-add src=portainer,target="/run/secrets/portainer" \
    portainer
```

服务将添加新密钥并加密数据库。

### 新安装：编辑compose文件

要在Docker Swarm上安装带加密的Portainer，需要编辑下载的compose文件作为安装过程的一部分。向`portainer`服务定义添加一个secrets部分：

```
secrets:
  - portainer
```

这告诉服务使用之前创建的`portainer`密钥。

此外，因为我们之前单独创建了它，所以需要将其指定为`external`，以便Docker知道在创建堆栈时不要创建它。为此，我们在`services:`定义之外为`portainer`密钥添加一个`secrets:`定义：

```
secrets:
  portainer:
    external: true
```

添加密钥后，您的完整Portainer堆栈文件可能如下所示：

```
version: '3.2'

services:
  agent:
    image: portainer/agent:lts
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
      - portainer

networks:
  agent_network:
    driver: overlay
    attachable: true

volumes:
  portainer_data:
      
secrets:
  portainer:
    external: true
```

保存更改，然后使用compose文件部署Portainer安装，如Swarm安装说明中所述。数据库将在安装过程中部署为加密状态。

## Kubernetes

要在Kubernetes上启用加密，首先需要创建一个密钥。然后您需要将此密钥作为卷挂载到Portainer中。

### 创建密钥

在Kubernetes集群的命令行中，可以运行以下命令创建密钥：

```
kubectl create secret generic portainer-key --from-literal=secret=我是一个密钥 --namespace portainer
```

将`我是一个密钥`替换为您的密钥。这将创建一个名为`portainer-key`的密钥，该密钥将用于加密Portainer数据库。

### 修改YAML文件

创建密钥后，我们需要修改YAML文件以将密钥作为卷挂载到Portainer中。下载适用于您特定部署的YAML文件并找到`portainer`容器的`container`定义。它应该如下所示：

```
containers:
  - name: portainer
    image: "portainer/portainer-ee:lts"
    imagePullPolicy: Always
    args:          
    volumeMounts:
      - name: data
        mountPath: /data  
```

在`volumeMounts`部分，为之前创建的密钥添加定义：

```
volumeMounts:
  - name: data
    mountPath: /data
  - name: portainer-key
    mountPath: /run/secrets/portainer
    subPath: portainer
```

我们还需要为`spec`的`volumes`定义添加定义：

```
spec:
  containers:
    portainer:
    ...
  volumes:
    - name: portainer-key
      secret:
        secretName: portainer-key
        items:
          - key: secret
            path: portainer
      
```

保存文件，然后将其应用到正在运行的配置中：

```
kubectl apply -f portainer.yaml
```

将`portainer.yaml`替换为您修改后的YAML文件的名称。
