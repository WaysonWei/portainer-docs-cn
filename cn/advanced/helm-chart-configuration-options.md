# Helm 图表配置选项

下表列出了 Portainer Helm 图表的可配置参数及其默认值。可在 `deploy/helm/portainer/values.yaml` 中找到对应的值文件。

| 参数                    | 描述                                                                                               | 默认值                     |
| ---------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------- |
| `replicaCount`               | Portainer 服务副本数（始终设置为1）。                                                   | `1`                         |
| `image.repository`           | Portainer Docker Hub 仓库地址。                                                                          | `portainer/portainer-ce`    |
| `image.tag`                  | Portainer 镜像标签。                                                                              | `latest`                    |
| `image.pullPolicy`           | Portainer 镜像拉取策略。                                                                           | `IfNotPresent`              |
| `imagePullSecrets`           | 如果 Portainer 镜像位于私有仓库中需要配置此项。                                               | `nil`                       |
| `nodeSelector`               | 用于为部署应用节点选择器。                                                           | `{}`                        |
| `serviceAccount.annotations` | 要添加到服务账户的注解。                                                                | `null`                      |
| `serviceAccount.name`        | 要使用的服务账户名称。                                                                   | `portainer-sa-clusteradmin` |
| `service.type`               | 主 Portainer 服务的类型。有效值：`ClusterIP`, `NodePort`, `LoadBalancer`。       | `LoadBalancer`              |
| `service.httpPort`           | 访问 Portainer Web 界面的 HTTP 端口。                                                      | `9000`                      |
| `service.httpNodePort`       | 访问 Portainer Web 界面的静态 NodePort。仅在类型为 `NodePort` 时指定。        | `30777`                     |
| `service.edgePort`           | 访问 Portainer Edge 的 TCP 端口。                                                                    | `8000`                      |
| `service.edgeNodePort`       | 访问 Portainer Edge 的静态 NodePort。仅在类型为 `NodePort` 时指定。                     | `30776`                     |
| `service.annotations`        | 要添加到服务的注解。                                                                        | `{}`                        |
| `ingress.enabled`            | 为 Portainer 创建 Ingress。                                                                         | `false`                     |
| `ingress.annotations`        | <p>要添加到 Ingress 的注解。例如：<br><code>kubernetes.io/ingress.class: nginx</code></p> | `{}`                        |
| `ingress.hosts.host`         | Portainer Web 的 URL。例如：`portainer.example.io`。                                               | `nil`                       |
| `ingress.hosts.paths.path`   | Portainer Web 界面的路径。                                                                     | `/`                         |
| `ingress.hosts.paths.port`   | Portainer Web 界面的端口。                                                                     | `9000`                      |
| `ingress.tls`                | Ingress 上的 TLS 支持。必须提前创建包含 TLS 证书的 Secret。                            | `[]`                        |
| `resources`                  | Portainer 资源请求和限制。                                                                   | `{}`                        |
| `persistence.enabled`        | 是否启用数据持久化。                                                                | `true`                      |
| `persistence.existingClaim`  | 用于数据持久化的现有 PVC 名称。                                                      | `nil`                       |
| `persistence.size`           | 用于持久化的 PVC 大小。                                                                     | `10Gi`                      |
| `persistence.annotations`    | 应用于持久化 PVC 的注解。                                                         | `{}`                        |
| `persistence.storageClass`   | 应用于持久化 PVC 的 StorageClass。                                                        | `default`                   |
| `persistence.accessMode`     | 持久化的访问模式。                                                                               | `ReadWriteOnce`             |
| `persistence.selector`       | 持久化的选择器。                                                                                 | `nil`                       |
