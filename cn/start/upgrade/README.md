# 更新 Portainer

Portainer 版本包含新功能和错误修复，因此保持安装最新非常重要。我们已经[测试并验证](../requirements-and-prerequisites.md#valid-configurations)了从 2.0.0 到最新版本的所有 Portainer 版本升级路径。

虽然未经测试的升级路径可能有效，但我们建议在应用到生产系统之前，先在非关键系统上测试和验证所有升级路径。

我们在 Portainer BE 2.7 中添加了[备份和恢复功能](../../admin/settings/#backup-portainer)，强烈建议在更新前备份您的 Portainer 实例。

从 CE 2.9 和 BE 2.10 开始，Portainer 默认启用 HTTPS 并使用端口 `9443` 提供 UI。如果需要，仍可在端口 `9000` 上启用 HTTP。

## 更新顺序

通常，我们建议在更新 Portainer Agent 之前先更新 Portainer Server 部署。当我们发布新版本的 Portainer 时，会确保 Portainer Server 能够与旧版本的 Agent 通信，在大多数情况下反之亦然，但在某些情况下，我们对 Agent 进行的更改与旧版本的 Portainer Server 不完全向后兼容。

## 更新 Portainer

### 从 Portainer 内部更新

目前不支持从 Portainer 内部更新到 STS 版本（或在 STS 版本之间更新）。只有 LTS 版本会通过应用内更新提供。要切换到 STS 版本或更新到 STS 版本，请按照下面的[手动说明](./#manually-update-portainer)操作。

从 2.19 开始，商业版用户可以直接从 Portainer 内部更新其安装。为此，请点击 Portainer UI 左下角更新通知中的**立即更新**链接。

<figure><img src="..//assets/2.19-update-notification.png" alt=""><figcaption></figcaption></figure>

在确认对话框中，点击**开始更新**继续更新。

记住在更新前[备份您的 Portainer 安装](../../admin/settings/#backup-portainer)！

<figure><img src="..//assets/2.19-update-confirmation.png" alt=""><figcaption></figcaption></figure>

### 手动更新 Portainer

如果您更愿意手动更新 Portainer 安装，请选择您的平台然后按照说明操作：

[docker.md](docker.md)

[swarm.md](swarm.md)

[podman.md](podman.md)

[kubernetes.md](kubernetes.md)

### 更新 Portainer Agent

要更新标准（非 Edge）Portainer Agent，您可以在上述平台特定链接中找到说明（[Docker 单机版](docker.md#agent-only-upgrade)、[Docker Swarm](swarm.md)、[Podman](podman.md) 和 [Kubernetes](kubernetes.md)）。

如果您使用 Portainer Edge Agent，我们有特定的更新说明：

[edge.md](edge.md)

### 升级到商业版

如果您来自 Portainer CE 或 1.24.x 分支，我们也有指南供您参考。

[tobe](tobe/)
