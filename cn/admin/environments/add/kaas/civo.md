# Civo

从提供商列表中选择**Civo**选项。如果尚未提供Civo API令牌，系统会要求您提供凭据详细信息。为凭据提供**名称**并将您的Civo API令牌粘贴到**API密钥**字段中，然后点击**添加凭据**。

您可以在[共享凭据文档](../../../settings/credentials/)中找到有关[设置Civo账户访问权限](../../../settings/credentials/civo.md)的更多详细信息。

<figure><img src="../../..//assets/2.21.2-kaas-create-civo-creds.png" alt=""><figcaption></figcaption></figure>

添加凭据后（或如果已设置凭据），从以下字段中选择集群选项。

| 字段/选项       | 概述                                                             |
| ------------------ | -------------------------------------------------------------------- |
| 名称               | 输入集群的名称。                                       |
| 凭据        | 选择用于配置的凭据集。              |
| 区域             | 选择部署集群的区域。                         |
| 节点大小          | 选择集群中单个节点的大小。             |
| 节点数量         | 输入集群中要配置的节点数。              |
| 网络ID         | 选择要添加集群的网络。                           |
| Kubernetes版本 | 选择要在集群上部署的Kubernetes版本。 |

您可以通过点击**操作**部分中的**重新加载集群详细信息**手动刷新Civo提供的选项。

### 关于Civo版本的注意事项

使用Kubernetes 1.27或更高版本在Extra Small节点大小上的Civo集群可能无法完成配置，因为计算资源对于所需工作负载来说太有限。1.27之前的版本没有此资源要求，因此可以与Extra Small节点大小一起使用。

<figure><img src="../../..//assets/2.21.2-kaas-create-civo-cluster.png" alt=""><figcaption></figcaption></figure>

您还可以展开**更多设置**部分，现在为环境设置组和标签，或者稍后再进行设置。

<figure><img src="../../..//assets/2.15-kaas-provision-moresettings.png" alt=""><figcaption></figcaption></figure>

完成选择后，点击**配置环境**开始配置。如果您还有其他环境需要配置，点击**下一步**继续，否则点击**关闭**返回环境列表，您将在其中看到配置进度。
