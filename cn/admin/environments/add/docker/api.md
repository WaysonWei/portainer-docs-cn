# 连接到Docker API

在开始之前，您需要确保您的Docker实例已配置为允许远程连接。要了解如何配置，请参考Docker官方文档。配置完成后，您可以选择使用或不使用TLS进行连接。

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

接下来，选择**Docker Standalone**作为环境类型，然后点击**开始向导**。选择**API**选项和您的平台，然后参考下表输入环境详细信息：

<table><thead><tr><th width="280">字段/选项</th><th>概述</th></tr></thead><tbody><tr><td>名称</td><td>为环境指定一个描述性名称。</td></tr><tr><td>Docker API URL</td><td>输入用于连接Docker主机的DNS名称或IP地址以及端口。不使用TLS连接时，默认端口为<code>2375</code>。使用TLS连接时，默认端口为<code>2376</code>。</td></tr><tr><td>TLS</td><td>如果要使用TLS，请切换此选项为开启状态。如果不想使用TLS，请切换为关闭状态。</td></tr><tr><td>跳过证书验证</td><td>切换此选项为开启状态以跳过对Docker API使用的TLS证书的验证。如果此选项关闭，以下字段将不会显示。</td></tr><tr><td>TLS CA证书</td><td>选择您的CA证书。</td></tr><tr><td>TLS证书</td><td>选择您的证书。</td></tr><tr><td>TLS密钥</td><td>选择与证书匹配的密钥。</td></tr></tbody></table>

Portainer期望TLS证书和密钥采用PEM格式。

<figure><img src="../../..//assets/2.18-environments-add-docker-api-details.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分，通过将环境添加到[组](../../groups.md)或[标记](../../tags.md)来分类环境以提高可搜索性。

GPU配置已移至[主机设置](../../../../user/docker/host/setup.md#other)，可以在环境设置完成后进行配置。

<figure><img src="../../..//assets/2.18-environments-add-docker-moresettings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**连接**。如果您有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表。
