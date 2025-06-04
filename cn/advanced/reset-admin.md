# 重置管理员密码

如果您的 Portainer 管理员忘记了密码，请按照以下步骤重置密码。根据您的 Portainer 环境，有三种方法可供选择。

## 方法 1：当 Portainer 作为容器运行时重置管理员密码

此方法通常适用于在 Docker Standalone 上运行 Portainer Server 的情况。

首先，访问我们的 [密码重置辅助容器](https://github.com/portainer/helper-reset-password) GitHub 页面，然后运行以下命令停止 Portainer 容器：

```
docker stop "id-portainer-container"
```

接下来，运行辅助容器（需要挂载 Portainer 数据卷）：

如果您的 Portainer 数据卷名称不是 `portainer_data` 或者您使用了绑定挂载作为数据卷，您需要调整以下 `docker run` 命令中的挂载路径以匹配您的配置。

```
docker pull portainer/helper-reset-password
docker run --rm -v portainer_data:/data portainer/helper-reset-password
```

如果成功，输出应如下所示：

```
2020/06/04 00:13:58 用户密码更新成功: admin
2020/06/04 00:13:58 请使用以下密码登录: &_4#\3^5V8vLTd)E"NWiJBs26G*9HPl1
```

如果辅助容器无法找到要更新的管理员用户，它将为您创建一个新用户。如果用户名 `admin` 已被使用，它将创建一个名为 `admin-[随机字符串]` 的用户：

```
2022/08/10 07:36:33 [警告] 无法获取 ID 为 1 的用户，将尝试创建，错误：数据库中未找到对象
2022/08/10 07:36:33 管理员用户 admin-u0512b3f0v4dqk7o 创建成功
2022/08/10 07:36:33 请使用以下密码登录: Sr#]YL_6D0k8Pd{pA9^|}F32j5J4I=av
```

最后，使用以下命令启动 Portainer 容器，然后尝试使用新密码登录：

```
docker start "id-portainer-container"
```

## 方法 2：当 Portainer 作为堆栈/服务运行时重置管理员密码

此方法通常适用于在 Docker Swarm 上运行 Portainer Server 的情况。

首先，使用以下命令将 Portainer 服务缩放到零：

```
docker service scale portainer_portainer=0
```

接下来，使用与数据卷相同的绑定挂载/卷运行 [密码重置辅助容器](https://github.com/portainer/helper-reset-password)：

如果您的 Portainer 数据卷名称不是 `portainer_portainer_data` 或者您使用了绑定挂载作为数据卷，您需要调整以下 `docker run` 命令中的挂载路径以匹配您的配置。

```
docker pull portainer/helper-reset-password
docker run --rm -v portainer_portainer_data:/data portainer/helper-reset-password
```

如果成功，输出应如下所示：

```
2020/06/04 00:13:58 用户密码更新成功: admin
2020/06/04 00:13:58 请使用以下密码登录: &_4#\3^5V8vLTd)E"NWiJBs26G*9HPl1
```

如果辅助容器无法找到要更新的管理员用户，它将为您创建一个新用户。如果用户名 `admin` 已被使用，它将创建一个名为 `admin-[随机字符串]` 的用户：

```
2022/08/10 07:36:33 [警告] 无法获取 ID 为 1 的用户，将尝试创建，错误：数据库中未找到对象
2022/08/10 07:36:33 管理员用户 admin-u0512b3f0v4dqk7o 创建成功
2022/08/10 07:36:33 请使用以下密码登录: Sr#]YL_6D0k8Pd{pA9^|}F32j5J4I=av
```

最后，使用以下命令启动 Portainer 服务，然后尝试使用新密码登录：

```
docker service scale portainer_portainer=1
```

## 方法 3：当 Portainer 部署在 Kubernetes 集群中时重置管理员密码

此方法通常适用于在 Kubernetes 集群上运行 Portainer Server 的情况。

首先，使用以下命令将 Portainer 部署缩放到零：

```
kubectl scale deploy portainer --replicas=0 -n portainer
```

接下来，创建一个使用 [密码重置辅助容器](https://github.com/portainer/helper-reset-password) 镜像的 Pod 并挂载 Portainer 数据卷。使用以下命令创建一个 Pod YAML 文件：

您可能需要更改下面的 YAML 以匹配您的 Portainer 部署（例如，如果使用不同的 `claimName`）。

```
cat > passreset.yml<< EOF
apiVersion: v1
kind: Pod
metadata:
  name: passreset
spec:
  volumes:
    - name: data
      persistentVolumeClaim:
        claimName: portainer
  containers:
    - name: passreset
      image: portainer/helper-reset-password
      volumeMounts:
        - mountPath: "/data"
          name: data
  restartPolicy: Never
EOF
```

使用以下命令创建密码重置 Pod：

```
kubectl apply -f passreset.yml -n portainer
```

一旦新 Pod 创建并转换为完成状态，您可以在 Pod 日志中看到新密码：

```
kubectl logs passreset -n portainer
```

如果成功，输出应如下所示：

```
2020/06/04 00:13:58 用户密码更新成功: admin
2020/06/04 00:13:58 请使用以下密码登录: &_4#\3^5V8vLTd)E"NWiJBs26G*9HPl1
```

最后，使用以下命令扩展 Portainer 部署，然后尝试使用新密码登录：

```
kubectl scale deploy portainer --replicas=1 -n portainer
```

您可以使用以下命令删除密码重置 Pod：

```
kubectl delete pod passreset -n portainer
