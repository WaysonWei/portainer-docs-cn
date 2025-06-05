# 构建说明

本文介绍如何设置本地开发环境以便为Portainer代码库做贡献。

请确保您已在[Mac](mac.md)或[Linux](linux.md)机器上安装此项目的依赖项后再继续。



Windows目前不被Portainer开发环境支持。


## 操作指南

导航到您将存储Portainer项目代码的文件夹。这可以是任何位置，例如您的桌面或下载文件夹。

现在，下载Portainer项目：

```
git clone https://github.com/portainer/portainer.git
```

接下来，进入您下载的Portainer项目目录：

```
cd portainer
```

安装开发依赖项：

```
make deps
```

最后，构建并运行项目：

```
make dev
```

您现在应该可以通过`https://localhost:9443`访问Portainer，UI开发服务器运行在`http://localhost:8999`。

如需其他命令，请运行`make help`。


前端应用程序会在您保存对任何源文件的更改时自动更新并刷新。


## 贡献指南

当为Portainer代码库做贡献时，请遵循[我们的贡献指南](https://github.com/portainer/portainer/blob/develop/CONTRIBUTING.md)。
