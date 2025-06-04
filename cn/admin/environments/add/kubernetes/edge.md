# 在Kubernetes上安装Edge Agent标准版

当远程环境无法直接从Portainer Server实例访问时，我们建议在远程环境上部署Portainer _Edge Agent_。这样您就可以从Portainer Server实例管理远程环境，而无需在环境中打开任何端口。与传统方式不同（服务器连接到Agent），Edge Agent会定期轮询Portainer Server检查是否有待处理任务，并相应执行。

有关Edge Agent工作原理的技术概述，请参阅我们的[高级文档](../../../../advanced/edge-agent.md)。

## 准备工作

Edge Agent需要在Portainer Server实例上开放两个端口：UI端口（通常在Kubernetes上为`9443`或`30779`，使用NodePort时）和隧道端口（使用Kubernetes和NodePort时为`8000`或`30776`）。隧道端口用于在Portainer Edge Agent和Portainer Server实例之间提供安全的TLS隧道。我们的安装说明默认配置Portainer Server监听这两个端口，您需要确保防火墙允许外部访问这些端口才能继续。

如果您的Portainer Server实例部署时启用了TLS，agent将使用HTTPS连接回Portainer。但如果Portainer实例使用自签名证书，则必须使用`-e EDGE_INSECURE_POLL=1`标志部署Edge Agent。如果不使用此标志部署Edge Agent，则agent将无法与Portainer Server实例通信。

此外，我们的说明假设您的环境满足[我们的要求](../../../../start/requirements-and-prerequisites.md)。虽然Portainer可能在其他配置下工作，但可能需要配置更改或功能受限。

## 部署

从菜单展开**环境相关**，点击**环境**，然后点击**添加环境**。

<figure><img src="../../..//assets/2.22-environments-add.gif" alt=""><figcaption></figcaption></figure>

选择**Kubernetes**然后点击**开始向导**。然后选择**Edge Agent标准版**选项。使用下表作为指南输入环境详细信息。

| 字段                           | 概述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 名称                            | 输入环境的名称。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Portainer API服务器URL        | 输入Portainer Server实例的URL和端口，这是从Edge环境看到的地址。如果使用FQDN，请确保DNS已正确配置以提供此地址。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Portainer隧道服务器地址 | <p>输入Portainer Server实例隧道服务器的地址和端口，这是从Edge环境看到的地址。如果使用FQDN，请确保DNS已正确配置以提供此地址。<br>在大多数情况下，这与Portainer API服务器URL地址相同，但没有协议且端口为<code>8000</code>。<br>此字段仅在Portainer商业版中可用。社区版用户请参考<a href="https://github.com/portainer/portainer/issues/6251">此GitHub问题</a>。</p> |

<figure><img src="../../..//assets/2.17-install-agent-edge-nameurl.png" alt=""><figcaption></figcaption></figure>

作为可选步骤，您可以展开**更多设置**部分并调整环境的轮询频率 - 这定义了此Edge Agent检查Portainer Server新任务的频率。默认为每5秒一次。您还可以通过将环境添加到[组](../../groups.md)或添加[标签](../../tags.md)来分类环境，以便更好地搜索。

<figure><img src="../../..//assets/2.15-edge_agent_more_settings.png" alt=""><figcaption></figcaption></figure>

准备就绪后，点击**创建**。如果您正在预置Edge Agent部署，现在可以检索加入令牌以用于部署。

<figure><img src="../../..//assets/2.18-environments-add-docker-edge-jointoken.png" alt=""><figcaption></figcaption></figure>

否则，使用下表作为指南完成新出现的字段。

| 字段/选项            | 概述                                                                                                                                        |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 环境变量   | 输入以逗号分隔的环境变量列表，这些变量将从部署agent的主机获取并提供给agent。 |
| 允许自签名证书 | 切换此选项以允许agent通过HTTPS连接到Portainer时使用自签名证书。                                           |

<figure><img src="../../..//assets/2.18-environments-add-docker-edge-envvars.png" alt=""><figcaption></figcaption></figure>

复制生成的命令并在Edge环境上运行该命令以完成安装。

如果您在Portainer Server实例上设置了自定义`AGENT_SECRET`（通过在启动Portainer Server容器时指定AGENT_SECRET环境变量），您**必须**记住在部署Edge Agent时以相同方式（作为环境变量）显式提供相同的密钥，在agent部署定义中：

`env:`\
&#x20; `- name: AGENT_SECRET`\
&#x20;   `value: yoursecret`

<figure><img src="../../..//assets/2.18-environments-add-k8s-edge-command.png" alt=""><figcaption></figcaption></figure>

如果您有另一个相同类型的Edge标准环境要部署，可以点击**添加另一个环境**。否则，如果您有其他环境需要配置，点击**下一步**继续，或点击**关闭**返回环境列表。
