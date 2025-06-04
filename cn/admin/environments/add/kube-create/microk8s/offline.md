# 离线安装

要在目标服务器离线或隔离网络的情况下执行MicroK8s环境创建，需要一些先决配置。这包括下载您希望安装的MicroK8s版本的安装文件、相关插件镜像和Portainer Agent镜像。

这是高级功能，需要具备Linux命令行的工作知识。如果您不需要执行MicroK8s环境的离线或隔离网络安装，我们建议遵循[标准流程](./)。

## 准备工作

与标准MicroK8s配置一样，Portainer需要root或无密码sudo SSH访问权限来访问要配置的服务器。在此SSH用户的主目录中，创建一个名为`microk8s`的目录，并在其中创建一个名为`images`的子目录。这是Portainer期望离线安装MicroK8s文件的位置。例如：

```
mkdir -p $HOME/microk8s
mkdir -p $HOME/microk8s/images
```

完成以下步骤后，请确保上述目录（及其中的文件）由Portainer将用于执行安装的SSH用户拥有。

您还需要确保已安装`snap`，因为这是MicroK8s安装所必需的。现代版本的Ubuntu应该预装了`snap`，但如果您需要单独安装，可以参考[snap文档](https://snapcraft.io/docs/installing-snap-on-ubuntu)。

## 下载MicroK8s

接下来您需要下载MicroK8s安装文件。以下示例下载1.27版本 - 如果您需要使用其他版本，请相应调整命令。

```
snap download microk8s --channel 1.27
snap download core20
```

这应该会下载4个文件 - 一个`.assert`文件和一个`.snap`文件，分别用于`microk8s`和`core20`。例如（您的确切文件名可能不同）：

```
core20_2318.assert
core20_2318.snap
microk8s_6743.assert
microk8s_6743.snap
```

将这些下载的文件移动到您之前创建的`microk8s`目录中，并将它们重命名为Portainer期望的文件名：

```
mv microk8s_*.snap $HOME/microk8s/microk8s.snap
mv microk8s_*.assert $HOME/microk8s/microk8s.assert
mv core20_*.snap $HOME/microk8s/core20.snap
mv core20_*.assert $HOME/microk8s/core20.assert
```

## 下载所需镜像

为了支持MicroK8s的必要插件，您需要预先下载用于配置插件的Docker镜像。确切的插件和版本取决于您安装的MicroK8s版本，可以在MicroK8s仓库的以下URL中找到（调整版本号以适应）：

```
https://github.com/canonical/microk8s/blob/1.27/build-scripts/images.txt
```

例如，对于1.27版本，您将需要以下内容：

```
docker.io/calico/cni:v3.25.0
docker.io/calico/kube-controllers:v3.25.0
docker.io/calico/node:v3.25.0
docker.io/cdkbot/hostpath-provisioner:1.4.2
docker.io/coredns/coredns:1.10.0
docker.io/library/busybox:1.28.4
registry.k8s.io/ingress-nginx/controller:v1.5.1
registry.k8s.io/metrics-server/metrics-server:v0.5.2
registry.k8s.io/pause:3.7
```

此外，您还需要Portainer Agent镜像 - 将`{PORTAINER_SERVER_VERSION}`替换为与您的Portainer Server安装匹配的版本号（例如`2.20.3`）：

```
docker.io/portainer/agent:{PORTAINER_SERVER_VERSION}
```

如果您希望在Portainer中使用[kubectl shell](../../../../../user/kubernetes/kubectl.md)功能，您可能还需要预先下载`kubectl-shell`镜像：

```
docker.io/portainer/kubectl-shell:latest
```

预先下载这些镜像的一种方法是使用已安装的Docker拉取镜像，然后将它们保存在预期的路径和文件名中。例如：

```
docker image pull docker.io/portainer/agent:2.20.3
docker image save docker.io/portainer/agent:2.20.3 -o "$HOME/microk8s/images/docker,io-portainer-agent_2.20.3.tar"
```

这需要对每个需要的镜像执行。一个简单的bash脚本，一旦填充了镜像列表，就可以执行此操作：

```
imageList=("docker.io/calico/cni:v3.25.0" "docker.io/calico/kube-controllers:v3.25.0" "docker.io/calico/node:v3.25.0" "docker.io/cdkbot/hostpath-provisioner:1.4.2" "docker.io/coredns/coredns:1.10.0" "docker.io/library/busybox:1.28.4" "registry.k8s.io/ingress-nginx/controller:v1.5.1" "registry.k8s.io/metrics-server/metrics-server:v0.5.2" "registry.k8s.io/pause:3.7" "docker.io/portainer/agent:2.20.3" "docker.io/portainer/kubectl-shell:latest")

for image in ${imageList[@]}; do
  docker image pull $image && docker image save $image -o "$HOME/microk8s/images/$(echo $image | sed 's/\//-/g' | sed 's/:/_/g').tar"
done
```

## 将文件复制到所有节点

如果您正在安装多节点集群，则`$HOME/microk8s`目录及其中的文件必须位于集群中所有节点的相同路径上。在执行此操作时，请确保目录和文件具有正确的所有者（Portainer将用于连接节点的SSH用户）。

## 开始安装

您现在可以按照Portainer中的[标准流程](./)创建MicroK8s集群，但启用**离线安装**切换。

<figure><img src="../../../..//assets/2.20.3-environments-add-k8s-create-offline-toggle.png" alt=""><figcaption></figcaption></figure>
