# 安全约束

Pod安全策略可用于定义工作负载在什么条件下可以运行。在Portainer中，我们通过[OPA Gatekeeper](https://github.com/open-policy-agent/gatekeeper)利用[Open Policy Agent](https://www.openpolicyagent.org/)来实现这一点。

策略是按环境配置的。要启用和配置安全策略，从菜单中选择一个Kubernetes环境，然后展开**集群**并点击**安全约束**。

这是高级功能，应谨慎应用。如果部署尝试创建不符合定义安全约束的Pod，可能不会立即明显看出约束是配置失败的原因。

<figure><img src="../..//assets/2.20-kubernetes-cluster-security.gif" alt=""><figcaption></figcaption></figure>

切换**启用Pod安全约束**以启用功能，然后切换您需要的功能并根据需要进行配置。

策略基于[Kubernetes安全策略参考](https://v1-21.docs.kubernetes.io/docs/concepts/policy/pod-security-policy/#policy-reference) - 有关每个选项的更多详细信息，请参阅Kubernetes文档。

<table><thead><tr><th width="370">字段/选项</th><th>概述</th></tr></thead><tbody><tr><td>限制运行特权容器</td><td>设置Pod中的任何容器是否可以启用特权模式。</td></tr><tr><td>限制主机命名空间</td><td>控制Pod容器是否可以共享进程ID命名空间和主机IPC命名空间。</td></tr><tr><td>限制主机网络端口</td><td>定义Pod可以使用的端口范围，按网络基础。</td></tr><tr><td>限制卷类型</td><td>定义可以使用的卷类型。卷类型的示例包括<code>configMap</code>、<code>downwardAPI</code>、<code>emptyDir</code>、<code>persistentVolumeClaim</code>、<code>secret</code>、<code>projected</code>、<code>hostPath</code>、<code>flexVolume</code>。</td></tr><tr><td>限制主机文件系统路径</td><td>定义使用hostPath卷时允许的主机路径。</td></tr><tr><td>限制驱动程序</td><td>定义可以使用的FlexVolume驱动程序。</td></tr><tr><td>要求只读根文件系统</td><td>指定容器必须以只读根文件系统运行。</td></tr><tr><td>限制用户和组ID</td><td>控制容器运行的用户ID或组ID，或添加的组ID。对于用户，指定<code>MustRunAs</code>以定义特定的用户ID范围，<code>MustRunAsNonRoot</code>以要求非root用户，或<code>RunAsAny</code>以允许作为任何用户运行。对于组，指定<code>MustRunAs</code>、<code>MayRunAs</code>或<code>RunAsAny</code>。</td></tr><tr><td>限制升级到root权限</td><td>控制用户权限并防止文件启用额外功能。</td></tr><tr><td>限制Linux功能</td><td>定义Pod可用的功能。设置允许的功能以指定容器可以使用的功能，并设置必须删除的功能以指定必须从容器中删除的权限。</td></tr><tr><td>限制SELinux安全上下文</td><td>控制容器的SELinux上下文。您可以指定级别、角色、类型和用户。</td></tr><tr><td>限制Proc挂载类型</td><td>定义容器使用的<code>/proc</code>挂载类型。选择<code>Default</code>或<code>Unmasked</code>。</td></tr><tr><td>限制AppArmor配置文件</td><td>控制容器使用的AppArmor配置文件。有关更多详细信息，请参阅<a href="https://v1-21.docs.kubernetes.io/docs/tutorials/clusters/apparmor/#podsecuritypolicy-annotations">AppArmor文档</a>。</td></tr><tr><td>限制seccomp配置文件</td><td>控制容器或Pod使用的seccomp配置文件。</td></tr><tr><td>限制sysctl配置文件</td><td>控制容器使用的sysctl配置文件。指定禁止Pod使用的sysctl。</td></tr></tbody></table>

完成配置后，点击**保存设置**以应用您的更改。
