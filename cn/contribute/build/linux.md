# 设置 Linux 构建环境

作为开源产品，我们鼓励用户编辑我们的代码并提交补丁。本文介绍如何在 Linux 上设置本地环境，以便您可以构建自己的 Portainer 副本并测试您的更改。


我们已在 Ubuntu 18.04.2 LTS 上测试了这些说明。有关其他系统的说明，请参阅下面的链接文档。


## 依赖项

* [Docker CE](https://docs.docker.com/install/) 是在您的机器上运行的 Docker 应用程序，用于启用 Docker 功能。最新版本不是此开发堆栈的要求，但我们建议保持最新以获得改进和安全修复。
* ​[Yarn](https://yarnpkg.com/en/docs/install#mac-stable) 是一个用于在系统上安装新软件包的包管理器，用于运行 Portainer 开发环境。
* [Node.JS](https://nodejs.org/en/download/) 是一个 JavaScript 包，用于构建利用网络的应用程序，如 Portainer。需要版本 18 或更高。
* [Golang](https://golang.org/dl/) 是我们用于构建大部分 Portainer 软件的开源语言。需要 Golang 版本 1.18。
* Wget 是一个用于通过 HTTP 和 FTP 等常见互联网协议检索文件的包。

## 第一部分：安装 Docker


以下说明在 Ubuntu 上运行，有关此系统和其他 Linux 发行版的最新说明，请阅读 [官方 Docker CE 文档](https://docs.docker.com/install/)。



在安装 Docker 之前，您必须配置 Docker 仓库。


### 步骤 1：配置 Docker 仓库

首先，使用以下命令更新系统的软件包：

```
sudo apt-get update
```

接下来，安装通过 HTTPS 使用仓库所需的软件包：

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

现在安装 Docker 的官方 GPG 密钥：

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

使用以下指纹确认您拥有正确的密钥：

`9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`

运行以下命令验证密钥指纹：
```
sudo apt-key fingerprint 0EBFCD88
```

正确的输出应该是：

```
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

最后，使用以下命令设置稳定版仓库：

```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### 步骤 2：安装 Docker


我们始终建议使用官方供应商的最新说明安装软件。此步骤基于 Docker 自己的 [Linux 上 Docker 安装说明](https://docs.docker.com/install/)。


首先，使用以下命令更新系统的软件包：

```
sudo apt-get update
```

接下来，安装 Docker 及其相关软件包：

```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

最后，验证 Docker 是否正确安装并在您的系统上运行。此命令应下载一个测试镜像，在容器中运行，打印信息消息后退出。

```
sudo docker run hello-world
```

## 第二部分：安装 Yarn


如果您运行的是 Ubuntu 以外的 Linux 发行版，请阅读 Yarn 自己的 [Linux 上 Yarn 安装说明](https://yarnpkg.com/en/docs/install)。



如果您在安装或使用 Yarn 时遇到问题，请阅读其 [官方文档](https://yarnpkg.com/en/docs/install#mac-stable)。


在终端中运行以下命令来配置系统的 Yarn 仓库：

```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

使用以下命令更新系统软件包并安装 Yarn：

```
sudo apt-get update && sudo apt-get install yarn
```

最后，在终端中运行以下命令确认 Yarn 安装成功：

```
yarn --version
```

当前 Yarn 版本应显示在终端中，表明它已成功安装并在您的系统上运行。

## 第三部分：安装或更新 Node.JS


此过程使用 NVM 安装 Node.JS（需要 Node.JS 版本 12 或更高）。NVM 允许在系统上安装多个不同版本的 Node.JS，并提供了在它们之间切换的简便方法。



如果您在安装或更新 Node.JS 时遇到问题，请阅读 NVM 的 [文档](https://github.com/creationix/nvm)。


首先，在终端中运行以下命令安装或更新到最新版本的 Node.JS：

```
nvm install node
```

最后，检查 Node 是否已安装在您的系统上：

```
node --version
```

最新版本的 Node.JS 现在应该会显示出来。

## 第四部分：使用 Linux tar 文件安装 Golang


必须安装 Go 1.17 版本。如果您要从旧版本升级，必须先 [移除现有版本](https://golang.org/doc/install#uninstall) 再安装 1.17 版本。有关最新的安装说明，请阅读 [Go 官方文档](https://golang.org/doc/install#install)。



如果您在安装或使用 Go 时遇到问题，请阅读其官方文档中的 [获取帮助](https://golang.org/doc/install#help) 部分。


首先，[下载](https://golang.org/dl/)适合您系统的 Go 版本。导航到下载位置后，使用以下命令将其解压到 `/usr/local` 目录：

```
sudo tar -C /usr/local -xzf go1.17.6.linux-amd64.tar.gz
```

接下来，将 `/usr/local/go/bin` 添加到您的 shell 配置文件的 PATH 环境变量中。以下是使用 bash 的示例：

```
echo "export PATH=$PATH:$HOME/go/bin:/usr/local/go/bin" >> ~/.bashrc
```


您可能需要注销并重新登录才能使此更改生效。


最后，按照 [Golang 官方文档](https://golang.org/doc/code.html#Testing) 中的 _测试安装_ 部分确保 Go 已正确安装。

## 第五部分：安装 Wget


如果您在安装或使用 Wget 时遇到问题，请阅读其 [文档](https://www.gnu.org/software/wget/manual/)。


要在 Linux 上安装 Wget，只需在终端中运行以下命令：
```
apt-get install wget
```
