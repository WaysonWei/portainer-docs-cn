# 设置 macOS 构建环境

作为开源产品，我们鼓励用户编辑我们的代码并提交补丁。本文介绍如何在 Mac 上设置本地环境，以便您可以构建自己的 Portainer 副本并测试您的更改。


我们已在 macOS 10.14.3 (Mojave) 上测试了这些说明。


## 依赖项

* [Docker for Mac](https://www.docker.com/products/docker-desktop) 安装 Docker 应用程序和其他 Docker 工具。最新版本不是此开发堆栈的要求，但我们建议保持最新以获得改进和安全修复。
* [Yarn](https://yarnpkg.com/en/docs/install#mac-stable) 是一个用于在系统上安装新软件包的包管理器，用于运行 Portainer 开发环境。
* [Node.JS](https://nodejs.org/en/download/) 是一个 JavaScript 包，用于构建利用网络的应用程序，如 Portainer。需要版本 18 或更高。
* [Golang](https://golang.org/dl/) 是我们用于构建大部分 Portainer 软件的开源语言。需要 Golang 版本 1.18。
* Wget 是一个用于通过 HTTP 和 FTP 等常见互联网协议检索文件的包。

## 第一部分：安装 Docker for macOS


Docker for macOS 需要 OSX Mountain Lion 或更高版本，否则将无法工作。请确保您拥有正确的版本后再继续。


### 步骤 1：安装 Docker


我们始终建议使用官方供应商的最新说明安装软件。此步骤基于 Docker 自己的 [macOS 上 Docker 安装说明](https://runnable.com/docker/install-docker-on-macos)。


[下载 Docker](https://www.docker.com/products/docker-desktop) 然后导航到 `Docker.dmg` 文件并双击打开。将 Docker 拖放到您的应用程序文件夹中。使用系统密码授权安装，然后等待 Docker 完成安装。

要检查 Docker 是否安装成功，双击应用程序文件夹中的 Docker 启动它。鲸鱼图标应出现在状态栏中，表示 Docker 正在运行且可访问。

### 步骤 2：检查安装的 Docker 版本

点击状态栏中的 Docker 图标，然后从菜单中选择 **About Docker Desktop**（或类似名称的菜单项，具体取决于您的 Docker 版本）。将打开一个窗口，显示当前 Docker 版本及其支持软件。

## 第二部分：安装 Yarn


此过程使用 Homebrew 包管理器。请访问[此处](https://brew.sh/)了解如何安装它。如果您不想使用 Homebrew，Yarn 提供了[一些替代方案](https://yarnpkg.com/en/docs/install#mac-stable)。



如果您在安装或使用 Yarn 时遇到问题，请阅读其[官方文档](https://yarnpkg.com/en/docs/install#mac-stable)。


在 macOS 终端中运行 `brew install yarn` 将安装 Yarn。要确认安装成功，请在 macOS 终端中运行 `yarn --version`。

如果成功，当前 Yarn 版本将显示在终端中，表明它已成功安装并在您的系统上运行。

## 第三部分：安装或更新 Node.JS


如果您使用 Homebrew 安装 Yarn，Node.JS 应该会自动随之安装。如果没有，您可以按照 [Node.JS 文档](https://nodejs.org/en/download/) 进行安装。



如果您在使用 Homebrew 安装或更新 Node.JS 时遇到问题，请阅读 [Homebrew 故障排除指南](https://docs.brew.sh/Common-Issues)。


要检查 Node.JS 是否已安装在您的系统上，请在终端中运行 `node --version`。当前 Node.JS 版本应显示出来。如果版本是 6 或更高，更新到最新版本是可选的（但我们建议这样做，因为保持最新是良好的做法）。

如果您运行的 Node.JS 版本低于 6，则必须升级才能运行 Portainer 开发环境。

如果 Yarn 是使用 Homebrew 安装的，请按照以下步骤更新 Node.JS：
