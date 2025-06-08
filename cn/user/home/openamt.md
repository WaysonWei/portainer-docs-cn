# OpenAMT

OpenAMT允许您从Portainer远程管理兼容的Edge设备，包括启动、停止、重启设备以及直接从Portainer UI访问设备控制台。

## 准备工作

要将Edge设备与OpenAMT关联，首先需要添加兼容设备。为此，请先根据您的环境类型[部署Edge Agent](../../admin/environments/add/)到目标设备。

Edge Agent在远程设备上设置并部署完成后，设备即可与OpenAMT关联。

## 关联设备

要将现有的Edge Agent部署与OpenAMT关联，从首页点击**与OpenAMT关联**按钮。

<figure><img src="..//assets/2.18-home-openamt-associate-button.png" alt=""><figcaption></figcaption></figure>

勾选要关联的设备，然后点击**关联设备**按钮。激活过程将开始。

<figure><img src="..//assets/2.18-home-openamt-associate-dialog.png" alt=""><figcaption></figcaption></figure>

激活完成后，您将返回首页。

## 与设备交互

当OpenAMT设备与Portainer中的Edge设备关联后，您可以直接与该设备交互。为此，转到首页并使用磁贴右侧的选项进行所需操作：

* **开机**：如果设备当前关闭，将启动设备。
* **关机**：如果设备当前运行，将关闭设备。
* **重启**：将重新启动设备。
* **KVM**：将与设备建立远程KVM(键盘、视频、鼠标)会话。
