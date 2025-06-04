# 添加新环境

Portainer除了可以管理其安装所在的本地环境外，还可以管理多个其他环境。

您可以选择连接到现有环境：

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Docker Standalone</strong></td><td>通过URL/IP、API或Socket连接到Docker Standalone</td><td></td><td><a href="docker/">docker</a></td><td><a href="../..//assets/card-docker.png">card-docker.png</a></td></tr><tr><td><strong>Docker Swarm</strong></td><td>通过URL/IP、API或Socket连接到Docker Swarm</td><td></td><td><a href="swarm/">swarm</a></td><td><a href="../..//assets/card-docker.png">card-docker.png</a></td></tr><tr><td><strong>Podman</strong></td><td>通过URL/IP或Socket连接到Podman</td><td></td><td><a href="podman/">podman</a></td><td><a href="../..//assets/podman-logo-tile.png">podman-logo-tile.png</a></td></tr><tr><td><strong>Kubernetes</strong></td><td>通过URL/IP或kubeconfig导入连接到Kubernetes环境</td><td></td><td><a href="kubernetes/">kubernetes</a></td><td><a href="../..//assets/card-kubernetes.png">card-kubernetes.png</a></td></tr><tr><td><strong>Azure ACI</strong></td><td>通过API连接到Azure ACI环境</td><td></td><td><a href="aci.md">aci.md</a></td><td><a href="../..//assets/card-aci.png">card-aci.png</a></td></tr></tbody></table>

或者设置新环境：

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>配置KaaS集群</strong></td><td>通过云提供商的Kubernetes即服务配置Kubernetes集群</td><td></td><td><a href="kaas/">kaas</a></td><td><a href="../..//assets/card-kaas-large.png">card-kaas-large.png</a></td></tr><tr><td><strong>创建Kubernetes集群</strong></td><td>在现有基础设施上创建Kubernetes集群</td><td></td><td><a href="kube-create/">kube-create</a></td><td><a href="../..//assets/card-kube-create-large.png">card-kube-create-large.png</a></td></tr></tbody></table>

您也可以通过Portainer API添加环境。

[api.md](api.md)
