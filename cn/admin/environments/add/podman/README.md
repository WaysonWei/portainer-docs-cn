# 添加Podman环境

将Podman主机连接到Portainer时，根据您的特定需求有几种不同的方法可供选择。您可以在Podman主机上安装Portainer Agent并通过代理连接，可以直接连接到Podman socket，也可以部署Portainer Edge Agent的标准或异步模式。

无论选择哪种方法，都需要满足一些通用要求：

* 在Podman主机上安装并运行CentOS 9和最新版本的Podman 5.x。其他Podman版本和Linux发行版可能有效，但我们目前仅支持上述配置。我们建议遵循Podman的[官方安装说明](https://podman.io/docs/installation#installing-on-linux)。
* 在Podman主机上具有sudo或root权限。

安装说明还假设您的环境满足以下条件：

* 您的环境满足[我们的要求](../../../../start/requirements-and-prerequisites.md)。虽然Portainer可能在其他配置下工作，但可能需要配置更改或功能受限。
* Podman以root身份运行。Portainer与rootless Podman可能有效，但目前不受官方支持。

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Agent</strong></td><td></td><td></td><td><a href="agent.md">agent.md</a></td><td><a href="../../..//assets/card-agent-large.png">card-agent-large.png</a></td></tr><tr><td><strong>Socket</strong></td><td></td><td></td><td><a href="socket.md">socket.md</a></td><td><a href="../../..//assets/card-socket-large.png">card-socket-large.png</a></td></tr><tr><td><strong>Edge Agent标准版</strong></td><td></td><td></td><td><a href="edge.md">edge.md</a></td><td><a href="../../..//assets/card-edgestd-large.png">card-edgestd-large.png</a></td></tr><tr><td><strong>Edge Agent异步版</strong></td><td></td><td></td><td><a href="edge-async.md">edge-async.md</a></td><td><a href="../../..//assets/card-edgeasync-large.png">card-edgeasync-large.png</a></td></tr></tbody></table>
