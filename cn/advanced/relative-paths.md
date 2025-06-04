# Portainer 中相对路径支持的工作原理

Portainer 商业版中的相对路径卷支持旨在提供一种方式来引用 Git 仓库中与您的 compose 文件一起提供的文件和目录，而无需知道它们部署到环境时将出现的绝对路径。

相对路径支持仅在 Portainer 商业版中可用，并且需要[从 Git 部署堆栈时启用](../user/docker/stacks/add.md#relative-path-volumes)才能应用本文内容。

其后台工作原理如下：

1. 在 Portainer 中，从 Git 仓库位置启动堆栈部署，选择**启用相对路径卷**并指定**本地(或网络)文件系统路径**。
2. Portainer 创建一个临时的解包容器，该容器绑定挂载在本地(或网络)文件系统路径字段中指定的路径。
3. 解包容器将 Git 仓库克隆到绑定挂载路径下的子目录中。
4. Portainer 使用提供的 compose 文件创建堆栈，将工作目录指定为 Git 仓库克隆后 compose 文件所在的位置。
5. 堆栈部署完成后，临时解包容器被移除。

要在您的 compose 文件中利用此功能，您可以以相对于 compose 文件的_相对_方式指定仓库内文件的引用。例如，想象这个简单的 nginx 部署：

```
.
├── docker-compose.yml
└── static
    └── index.html
```

在此示例中，`docker-compose.yml` 文件位于仓库的根目录。旁边有一个名为 `static` 的目录，其中包含一个 `index.html` 文件。

`docker-compose.yml` 文件如下所示：

```
version: '3.1'
services:
  webapp:
    image: nginx:latest
    restart: always
    ports:
      - "3002:80"
    volumes:
      - ./static:/usr/share/nginx/html
```

最后一行是这里的重要部分 - 您会注意到我们引用 static 目录时使用了前导的 `.` 和 `/` - 这告诉 compose 指定的路径是_相对于_工作目录的，Portainer 在部署期间指定了工作目录。如果我们省略前导的 `.`，这将是一个_绝对_路径，并指向主机文件系统的 `/static`。

让我们看一个示例，其中您的 compose 文件位于仓库的子目录中，而您的内容位于不同的子目录中：

```
.
├── nginx
│   └── docker-compose.yml
└── static
    └── index.html
```

在此场景中，您将在部署时将 compose 文件指定为 `nginx/docker-compose.yml`。Portainer 会将仓库内容拉取到指定位置，并将工作目录设置为 compose 文件的位置(即 `nginx` 子目录内)。因此，compose 中的相对引用需要意识到这一点。要挂载 `static` 目录的内容，您的 compose 文件应如下所示：

```
version: '3.1'
services:
  webapp:
    image: nginx:latest
    restart: always
    ports:
      - "3002:80"
    volumes:
      - ../static:/usr/share/nginx/html
```

双点(`..`)表示文件位于工作目录上一级的目录中。

### 关于本地(或网络)文件系统路径的说明

Git 仓库克隆到的本地(或网络)文件系统路径将位于：

```
portainer-compose-unpacker/stacks/yourstackname/
```

例如，如果您部署了一个名为 `nginx` 的堆栈，并指定本地文件系统路径为：

```
/mnt/stacks/
```

结果将是：

```
/mnt/stacks/portainer-compose-unpacker/stacks/nginx/
```

这对于相对路径引用通常不相关，因为工作目录的定义避免了需要了解此完整路径，但这确实意味着可以使用相同的本地(或网络)文件系统路径来部署多个堆栈，而不用担心冲突(只要它们不共享相同的堆栈名称)。

此路径是您的堆栈挂载文件的来源位置，因此您需要确保此路径保持完整且不变。当使用此方法部署的堆栈被移除时，该堆栈的文件和目录结构也将被移除。
