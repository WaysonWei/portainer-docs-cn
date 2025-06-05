# Edge计算

要在Portainer中启用和配置Edge计算功能，从菜单中选择**设置**，然后选择**Edge计算**。

要了解如何使用我们的Edge计算功能，请参阅本文档的[Edge计算](../../user/edge/)部分。

<figure><img src="..//assets/2.15-settings-edgecompute.gif" alt=""><figcaption></figcaption></figure>

## Edge计算设置

在本节中，您可以使用以下选项在Portainer中启用和配置Edge计算功能。

| Field/Option                               | Overview                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 启用Edge计算功能               | 切换此选项以启用Edge计算功能，包括Edge设备功能。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Portainer API服务器URL                   | <p>输入您的Portainer Server实例的默认URL和端口，如从Edge环境中看到的那样。如果使用FQDN，请确保DNS已正确配置。<br>手动部署Edge Agent时可以覆盖此值。<br>此功能仅在Portainer商业版中可用。</p>                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Portainer隧道服务器地址            | <p>输入您的Portainer Server实例隧道服务器的默认地址和端口，如从Edge环境中看到的那样。如果使用FQDN，请确保DNS已正确配置。<br>在大多数情况下，这与Portainer API服务器URL地址相同，但没有协议且端口为<code>8000</code>。<br>手动部署Edge Agent时可以覆盖此值。<br>此功能仅在Portainer商业版中可用。社区版用户请参考<a href="https://github.com/portainer/portainer/issues/6251">此GitHub问题</a>。</p> |
| 使用单独的mTLS证书                     | <p>启用此切换以使用单独的mTLS证书进行Edge Agent通信。禁用此选项时，Edge Agent将使用与Portainer UI相同的TLS证书。<br>有关mTLS的更多信息，请阅读我们的<a href="../../advanced/mtls.md">高级文档</a>。</p>                                                                                                                                                                                                                                                                                                                                 |
| TLS CA证书                         | 当**使用单独的mTLS证书**启用时，选择并上传用于mTLS的CA证书。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| TLS证书                            | 当**使用单独的mTLS证书**启用时，选择并上传用于mTLS的服务器证书。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| TLS密钥                                    | 当**使用单独的mTLS证书**启用时，选择并上传与服务器证书对应的密钥。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 强制使用Portainer生成的Edge ID | 启用此选项以要求Edge Agent部署使用的Edge ID必须存在于Portainer数据库中(即已创建具有匹配ID的环境)才能连接。                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

<figure><img src="..//assets/2.20-settings-edge-edgecompute.png" alt=""><figcaption></figcaption></figure>

完成后，点击**保存设置**。

如果您添加或更改了mTLS CA证书，需要重新启动Portainer Server才能使更改生效。您还应确保任何使用mTLS的Edge Agent也更新为使用新的CA证书。


## 部署同步选项

本节定义Edge Agent与Portainer Server实例同步的选项。

### 检查间隔

| 字段/选项                      | 概述                                                                                   |
| --------------------------------- | ------------------------------------------------------------------------------------------ |
| Edge Agent默认轮询频率 | 选择标准模式下的Edge Agent与Portainer Server实例检查的频率。 |

<figure><img src="..//assets/2.18-settings-edge-checkin.png" alt=""><figcaption></figcaption></figure>

### 异步检查间隔

以下选项适用于以异步模式部署的Edge Agent。

| 字段/选项                          | 概述                                                                                                  |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Edge Agent默认ping频率     | 选择异步模式下的Edge Agent向Portainer Server实例ping的频率。                    |
| Edge Agent默认快照频率 | 选择异步模式下的Edge Agent向Portainer Server实例更新快照的频率。      |
| Edge Agent默认命令频率  | 选择异步模式下的Edge Agent向Portainer Server实例检查待处理命令的频率。 |

<figure><img src="..//assets/2.17-settings-edge-asynccheckin.png" alt=""><figcaption></figcaption></figure>

## Edge计算访问

本节允许您通过使用**Edge管理员**角色来配置对Edge计算环境的访问。Edge管理员角色赋予用户对所有Edge环境中Edge资源的全面控制权，但不提供对Portainer其他部分的完全管理访问权限。

<figure><img src="..//assets/2.20-settings-edge-access.png" alt=""><figcaption></figcaption></figure>

要添加用户为Edge管理员，从**选择用户**下拉菜单中选择用户名，然后点击**创建访问**。

要从Edge管理员角色中移除用户，在Edge管理员列表中勾选用户名旁边的复选框，然后点击**移除**。

## 自动Edge环境创建

在本节中，您可以配置自动Edge环境配置的功能。

| 字段/选项                         | 概述                                                                                                                                                                                                                                                                           |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 启用Edge环境等待室 | 切换此选项以启用Edge设备的[等待室](../../user/edge/waiting-room.md)功能。这将允许任何连接到Portainer实例的Edge设备自动与Portainer关联。我们建议保持此选项开启(等待室启用)。 |

<figure><img src="..//assets/2.20-settings-edge-aeec.png" alt=""><figcaption></figcaption></figure>

## Intel OpenAMT

本节控制Portainer中[Intel OpenAMT](../../user/home/openamt.md)功能的配置。

| 字段/选项                         | 概述                                                                                                                                                                                                                                          |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 启用OpenAMT                       | 切换此选项以启用Portainer的OpenAMT功能。这只能在**启用Edge计算功能**开启时启用，启用后将显示以下字段。                                                        |
| MPS服务器                           | 输入您的MPS服务器的FQDN或IP地址。                                                                                                                                                                                                  |
| MPS用户                             | 输入用于连接MPS服务器的用户名。                                                                                                                                                                                            |
| MPS密码                         | 输入上述MPS用户的密码。密码必须为8-32个字符，包含至少一个大写字母、至少一个小写字母、至少一个数字和至少一个特殊字符。    |
| 域名                          | 输入与配置证书关联的完全限定域名。                                                                                                                                                               |
| 配置证书文件(.pfx) | <p>点击<strong>上传文件</strong>上传您的PFX格式证书。PFX必须包含私钥。在基于AMT 15的设备上必须使用SHA2。</p><p></p><p>当前支持的CA包括Comodo、DigiCert、Entrust和GoDaddy。</p> |
| 配置证书密码    | 输入配置证书的密码。密码必须为8-32个字符，包含至少一个大写字母、至少一个小写字母、至少一个数字和至少一个特殊字符。  |

<figure><img src="..//assets/2.15-settings-edgecompute-openamt.png" alt=""><figcaption></figcaption></figure>

完成更改后，点击**保存设置**。
