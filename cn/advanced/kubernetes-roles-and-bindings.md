# Kubernetes 角色和绑定

基于角色的访问控制仅在 Portainer 商业版中可用。

当使用 Portainer 管理 Kubernetes 环境时，基于角色的访问控制(RBAC)配置基于两个组件：

* Kubernetes 的集群角色和命名空间角色（限制对 Kubernetes 本身的访问）
* Portainer 的授权标志（[限制访问](kubernetes-roles-and-bindings.md#portainer-access-restrictions) Portainer 的功能）

以下表格提供了我们的 Portainer 角色如何映射到 Kubernetes 内能力的参考。

## 角色分配 <a href="#role-allocations" id="role-allocations"></a>

| Portainer 角色            | 集群角色绑定                                                                                                                                 | 命名空间角色绑定                                                                                                                                          |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 环境管理员 | cluster-admin (k8s 系统)                                                                                                                           | N/A                                                                                                                                                             |
| 操作员                  | [portainer-operator](kubernetes-roles-and-bindings.md#portainer-operator), [portainer-helpdesk](kubernetes-roles-and-bindings.md#portainer-helpdesk) | [portainer-view](kubernetes-roles-and-bindings.md#portainer-view) (所有非系统命名空间)                                                                   |
| 用户                      | [portainer-basic](kubernetes-roles-and-bindings.md#portainer-basic)                                                                                  | [portainer-edit](kubernetes-roles-and-bindings.md#portainer-edit), [portainer-view](kubernetes-roles-and-bindings.md#portainer-view) (仅分配的命名空间) |
| 帮助台                  | [portainer-helpdesk](kubernetes-roles-and-bindings.md#portainer-helpdesk)                                                                            | [portainer-view](kubernetes-roles-and-bindings.md#portainer-view) (所有非系统命名空间)                                                                   |
| 只读用户                 | [portainer-basic](kubernetes-roles-and-bindings.md#portainer-basic)                                                                                  | [portainer-view](kubernetes-roles-and-bindings.md#portainer-view) (仅分配的命名空间)                                                                    |

## 集群角色 <a href="#cluster-roles" id="cluster-roles"></a>

### portainer-basic <a href="#portainer-basic" id="portainer-basic"></a>

| API 组         | 资源               | 操作     |
| ----------------- | ----------------------- | --------- |
| (空)           | namespaces, nodes       | get, list |
| storage.k8s.io    | storageclasses          | list      |
| metrics.k8s.io    | namespaces, pods, nodes | get, list |
| networking.k8s.io | ingressclasses          | list      |

### portainer-helpdesk <a href="#portainer-helpdesk" id="portainer-helpdesk"></a>

| API 组         | 资源                                               | 操作            |
| ----------------- | ------------------------------------------------------- | ---------------- |
| (空)           | componentstatuses, endpoints, events, namespaces, nodes | get, list, watch |
| storage.k8s.io    | storageclasses                                          | get, list, watch |
| networking.k8s.io | ingresses                                               | get, watch       |
| networking.k8s.io | ingressclasses                                          | list             |
| metrics.k8s.io    | pods, nodes, nodes/stats, namespace                     | get, list, watch |

### portainer-operator <a href="#portainer-operator" id="portainer-operator"></a>

| API 组      | 资源                             | 操作            |
| -------------- | ------------------------------------- | ---------------- |
| (空)        | configmaps                            | update           |
| (空)        | pods                                  | delete           |
| apps           | daemonsets, deployments, statefulsets | patch            |
| metrics.k8s.io | pods, nodes, nodes/stats, namespaces  | get, list, watch |

## 命名空间角色 <a href="#namespace-roles" id="namespace-roles"></a>

### portainer-edit <a href="#portainer-edit" id="portainer-edit"></a>

| API 组         | 资源                                                                                                                                                                                                           | 操作                                           |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| (空)           | configmaps, endpoints, persistentvolumeclaims, pods, pods/attach, pods/exec, pods/portforward, pods/proxy, replicationcontrollers, replicationcontrollers/scale, secrets, serviceaccounts, services, services/proxy | create, delete, deletecollection, patch, update |
| (空)           | pods/attach, pods/exec, pods/portforward, pods/proxy, secrets, services/proxy                                                                                                                                       | get, list, watch                                |
| apps              | daemonsets, deployments, deployments/rollback, deployments/scale, replicasets, replicasets/scale, statefulsets, statefulsets/scale                                                                                  | create, delete, deletecollection, patch, update |
| autoscaling       | horizontalpodautoscalers                                                                                                                                                                                            | create, delete, deletecollection, patch, update |
| batch             | cronjobs, jobs                                                                                                                                                                                                      | create, delete, deletecollection, patch, update |
| extensions        | daemonsets, deployments, deployments/rollback, deployments/scale, ingresses, networkpolicies, replicasets, replicasets/scale, replicationcontrollers/scale                                                          | create, delete, deletecollection, patch, update |
| networking.k8s.io | ingresses, networkpolicies                                                                                                                                                                                          | create, delete, deletecollection, patch, update |
| policy            | poddisruptionbudgets                                                                                                                                                                                                | create, delete, deletecollection, patch, update |

### portainer-view <a href="#portainer-view" id="portainer-view"></a>

| API 组         | 资源                                                                                                                                                                                                                                                                                                                                                                   | 操作            |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| (空)           | bindings, componentstatuses, configmaps, endpoints, events, limitranges, namespaces, namespaces/status, persistentvolumeclaims, persistentvolumeclaims/status, pods, pods/log, pods/status, replicationcontrollers, replicationcontrollers/scale, replicationcontrollers/status, resourcequotas, resourcequotas/status, secrets, serviceaccounts, services, services/status | get, list, watch |
| apps              | controllerrevisions, daemonsets, daemonsets/status, deployments, deployments/scale, deployments/status, replicasets, replicasets/scale, replicasets/status, statefulsets, statefulsets/scale, statefulsets/status                                                                                                                                                           | get, list, watch |
| autoscaling       | horizontalpodautoscalers, horizontalpodautoscalers/status                                                                                                                                                                                                                                                                                                                   | get, list, watch |
| batch             | cronjobs, cronjobs/status, jobs, jobs/status                                                                                                                                                                                                                                                                                                                                | get, list, watch |
| extensions        | daemonsets, daemonsets/status, deployments, deployments/scale, deployments/status, ingresses, ingresses/status, networkpolicies, replicasets, replicasets/scale, replicasets/status, replicationcontrollers/scale                                                                                                                                                           | get, list, watch |
| networking.k8s.io | ingresses, ingresses/status, networkpolicies                                                                                                                                                                                                                                                                                                                                | get, list, watch |
| policy            | poddisruptionbudgets, poddisruptionbudgets/status                                                                                                                                                                                                                                                                                                                           | get, list, watch |

## Portainer 访问限制 <a href="#portainer-access-restrictions" id="portainer-access-restrictions"></a>

| 功能                    | 端点管理员 | 操作员           | 帮助台           | 标准用户      | 只读用户     |
| --------------------------- | -------------- | ------------------ | ------------------ | ------------------ | ------------------ |
| 命名空间范围             | 全部            | 全部，除系统外 | 全部，除系统外 | 默认 + 分配的 | 默认 + 分配的 |
| 命名空间                  | 读写             | 读                  | 读                  | 读                  | 读                  |
| 命名空间详情           | 读写             | 读                  | 读                  | 读                  | 读                  |
| 命名空间访问管理 | 读写             |                    |                    |                    |                    |
| 应用                | 读写             | 读                  | 读                  | 读写                 | 读                  |
| 应用详情         | 读写             | 读                  | 读                  | 读写                 | 读                  |
| Pod 删除                  | 是            | 是                |                    |                    |                    |
| 应用控制台         | 读写             | 读写                 |                    |                    |                    |
| 高级部署         | 读写             |                    |                    | 读写                 |                    |
| ConfigMaps & Secrets        | 读写             | 读                  | 读                  | 读写                 | 读                  |
| ConfigMap & Secret 详情  | 读写             | 读写                 | 读                  | 读写                 | 读                  |
| 卷                     | 读写             | 读                  | 读                  | 读写                 | 读                  |
| 卷详情              | 读写             | 读                  | 读                  | 读写                 | 读                  |
| 集群                     | 读写             | 读                  | 读                  |                    |                    |
| 集群节点视图           | 读写             | 读                  | 读                  |                    |                    |
| 集群设置               | 读写             |                    |                    |                    |                    |
| 应用错误详情   | 读              | 读                  | 读                  |                    |                    |
| 存储类禁用      | 读              | 读                  | 读                  |                    |                    |

## 社区版

以下表格涵盖了 Portainer 社区版(CE)中可用的两个角色。请注意 Portainer CE 中没有 Portainer 访问限制。

| Portainer 角色 | 集群角色绑定                                                    | 命名空间角色绑定                            |
| -------------- | ----------------------------------------------------------------------- | ------------------------------------------------- |
| 管理员          | (无限制)                                                        | (无限制)                                  |
| 用户           | [portainer-cr-user](kubernetes-roles-and-bindings.md#portainer-cr-user) | edit (默认 k8s 角色，仅分配的命名空间) |

### portainer-cr-user

| API 组         | 资源         | 操作 |
| ----------------- | ----------------- | ----- |
| (空)           | namespaces, nodes | list  |
| storage.k8s.io    | storageclasses    | list  |
| networking.k8s.io | ingresses         | list  |
