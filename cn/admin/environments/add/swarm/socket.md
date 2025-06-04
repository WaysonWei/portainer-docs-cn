# 连接到Docker Socket

在Swarm环境中连接到Docker socket是一个遗留选项，不建议用于新安装。我们强烈建议改用[Portainer Agent](agent.md)。

直接连接到Docker socket只能从本地环境完成。在开始之前，请确保运行Portainer Server容器的用户具有访问Docker socket的权限。

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

接下来，选择**Docker Swarm**作为环境类型，然后点击**开始向导**。选择**Socket**选项和您的平台。您将看到需要作为Portainer容器部署的一部分传递给Portainer Server的必要参数。

<figure><img src="../../..//assets/2.18-environments-add-swarm-socket-command.png" alt=""><figcaption></figcaption></figure>

根据下表填写字段：

<table><thead><tr><th width="280">字段/选项</th><th>概述</th></tr></thead><tbody><tr><td>名称</td><td>为环境指定一个描述性名称。</td></tr><tr><td>覆盖默认socket路径</td><td>切换此选项为开启状态以覆盖默认的<code>/var/run/docker.sock</code> socket路径。</td></tr><tr><td>Socket路径</td><td>如果<strong>覆盖默认socket路径</strong>已启用，请输入Docker socket的路径。</td></tr></tbody></table>

确保如果您更改了Socket路径，请相应地更新上面所需的绑定挂载参数。

<figure><img src="../../..//assets/2.18-environments-add-docker-socket-details.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分，通过将环境添加到[组](../../groups.md)或[标记](../../tags.md)来分类环境以提高可搜索性。

<figure><img src="../../..//assets/2.18-environments-add-docker-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
