# 连接到Podman Socket

直接连接到Podman socket只能从本地环境完成。开始之前，请确保运行Portainer Server容器的用户有权访问Podman socket。

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

接下来，选择**Podman**作为环境类型，然后点击**开始向导**。选择**Socket**选项和您的平台。您将看到确保已启动Podman socket所需的命令。

<figure><img src="../../..//assets/2.22.0-environments-add-podman-socket.png" alt=""><figcaption></figcaption></figure>

根据下表填写字段。

<table><thead><tr><th width="280">字段/选项</th><th>概述</th></tr></thead><tbody><tr><td>名称</td><td>为环境指定一个描述性名称。</td></tr><tr><td>覆盖默认socket路径</td><td>切换此选项以覆盖默认socket路径。</td></tr><tr><td>Socket路径</td><td>如果启用了<strong>覆盖默认socket路径</strong>，请输入Podman socket的路径。</td></tr></tbody></table>

<figure><img src="../../..//assets/2.22.0-environments-add-podman-socket-2.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分，通过将环境添加到[组](../../groups.md)或添加[标签](../../tags.md)来分类环境，以便更好地搜索。

<figure><img src="../../..//assets/2.18-environments-add-docker-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您还有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
