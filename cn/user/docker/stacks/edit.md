# 检查或编辑堆栈

## 检查堆栈

从菜单选择**堆栈**，然后选择要检查的堆栈。

<figure><img src="../..//assets/2.20-stacks-edit.gif" alt=""><figcaption></figcaption></figure>

在这里可以停止、删除或[从堆栈创建模板](template.md)，如果从Git部署，还可以[将堆栈与Git仓库分离](edit.md#detach-from-git)。

<figure><img src="../..//assets/2.20-stacks-edit-options.png" alt=""><figcaption></figcaption></figure>

如果堆栈是从Git仓库部署的，可以：

* 配置[GitOps更新](add.md#gitops-updates)或手动拉取并重新部署堆栈。
* 查看和编辑堆栈的环境变量。

<figure><img src="../..//assets/2.20-stacks-edit-git.png" alt=""><figcaption></figcaption></figure>

如果堆栈是使用[Web编辑器](add.md#option-1-web-editor)或[上传](add.md#option-2-upload)部署的，将可以选择[手动编辑compose文件](edit.md#editing-a-stack)。

无论使用何种部署方法，还可以[迁移或复制](migrate.md)堆栈。

### Docker Standalone / Podman

使用Docker Standalone或Podman时，可以：

* 查看组成堆栈的容器。
* 检查它们是运行还是停止。
* 访问日志。
* 检查单个容器。
* 查看容器统计信息。
* 访问容器的控制台。

还可以看到堆栈中每个容器的镜像更新指示器。要重新检查堆栈中所有容器的镜像更新状态，可以点击搜索框旁边的重新加载按钮，或者要重新检查单个容器的镜像，点击该容器的镜像更新指示器图标。

<figure><img src="../..//assets/2.20-stacks-edit-containers.png" alt=""><figcaption></figcaption></figure>

### Docker Swarm

使用Docker Swarm时，可以：

* 查看组成堆栈的服务，以及组成每个服务的单个任务。
* 检查它们是运行还是停止。
* 查看每个主机上运行的副本数量。
* 访问日志。
* 检查单个服务。
* 查看服务统计信息。
* 访问服务的控制台。

还可以看到堆栈中每个服务的镜像更新指示器。要重新检查堆栈中所有服务的镜像更新状态，可以点击"重新加载镜像指示器"按钮，或者要重新检查单个服务的镜像，点击该服务的镜像更新指示器图标。

<figure><img src="../..//assets/2.20-stacks-edit-services.png" alt=""><figcaption></figcaption></figure>

## 编辑堆栈

编辑堆栈允许更改配置并重新部署这些更改。要编辑堆栈，从菜单选择**堆栈**，选择要编辑的堆栈，然后选择**编辑器**选项卡。

编辑器选项卡仅适用于使用[Web编辑器](add.md#option-1-web-editor)部署的堆栈。对于从Git仓库部署的堆栈，必须在仓库本身中编辑compose文件。

<figure><img src="../..//assets/2.19-stacks-edit-webeditor.png" alt=""><figcaption></figcaption></figure>

在这里，可以根据需要编辑堆栈的Compose文件。使用**版本**下拉菜单，还可以选择堆栈文件的先前版本(如果存在)以根据需要切换回去。从下拉菜单中选择不同的版本将用所选版本的内容替换编辑器的内容。

随时可以按`Ctrl-F`(Mac上是`Cmd-F`)在Web编辑器中搜索。

在此部分可以展开"环境变量"部分以查看和更改堆栈的环境变量。

<figure><img src="../..//assets/2.20-stacks-edit-envvars.png" alt=""><figcaption></figcaption></figure>

还可以切换堆栈[webhook](webhooks.md)并检索webhook URL：

<figure><img src="../..//assets/2.20-stacks-edit-webhook.png" alt=""><figcaption></figcaption></figure>

如果进行了从堆栈中删除某些服务的更改，可以选择**清理服务**。

<figure><img src="../..//assets/2.20-stacks-edit-swarm-prune.png" alt=""><figcaption></figcaption></figure>

完成更改后，点击**更新堆栈**。

## 从Git分离

如果堆栈是从Git仓库创建的，可以选择将堆栈与仓库分离。这意味着可以[直接在Portainer中编辑堆栈](edit.md#editing-a-stack)，但也意味着堆栈不能再从Git更新。此操作也无法撤销。

分离会下载堆栈的主要compose文件并将其存储在Portainer中。它不会下载仓库中可能包含的任何其他compose文件或`.env`文件。

点击**从Git分离**进行分离。系统会要求确认操作 - 点击**分离**执行操作。
