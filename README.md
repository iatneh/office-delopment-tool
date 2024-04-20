# 定制Office组件镜像包

[Office Deployment Tool 官网网站](https://learn.microsoft.com/zh-cn/deployoffice/office2019/deploy)


## 文件列表
* `setup.exe` cli执行文件，由[officedeploymenttool_17531-20046.exe](https://download.microsoft.com/download/2/7/A/27AF1BE6-DD20-4CB4-B154-EBAB8A7D4A7E/officedeploymenttool_17531-20046.exe)安装后可得，有需要也可以从官网下载最新版
* `configuration-example` 配置文件模板，由[officedeploymenttool_17531-20046.exe](https://download.microsoft.com/download/2/7/A/27AF1BE6-DD20-4CB4-B154-EBAB8A7D4A7E/officedeploymenttool_17531-20046.exe)安装后可得，有需要也可以从官网下载最新版
* `configuration-2019.xml` Office2019 组件配置文件，可以自行增减产品，`Product`下的`ExcludeApp`可以[生成配置](https://config.office.com/deploymentsettings)后，导出到本地，把对应的`ExcludeApp`拷贝过来
* `install.bat` 自定义镜像中使用，挂载镜像后可以执行此脚本安装

## `configuration-2019.xml`产品列表
> [ExcludeApp 元素](https://learn.microsoft.com/zh-cn/deployoffice/office-deployment-tool-configuration-options#excludeapp-elements)

* 保留 Excel、Word、PowerPoint、Outlook、Visio、Project
* 排除 Access、OneDrive(Groove)、Skype for Business、OneDrive Desktop、OneNote、Publisher

## 使用CMD执行setup命令行
### 查看setup帮助
~~~cmd
setup -h

Office Deployment Tool

Setup [mode] [path]

Setup /download [path to configuration file]
Setup /configure [path to configuration file]
Setup /packager [path to configuration file] [output path]
Setup /customize [path to configuration file]
Setup /help

 /download Downloads files to create an Office installation source
 /configure Adds, removes, or configures an Office installation
 /packager Produces an Office App-V package from an Office installation source
 /customize Applies settings for Office applications
 /help Displays this message
~~~

### 预下载文件
~~~cmd
## 如果只想安装，则不必执行，如果要制作自己的镜像文件，需要进行预下载
## 把配置文件中的产品文件预下载到当前路径`Office`文件夹
setup /download configuration-2019.xml
~~~

### 直接执行安装
~~~cmd
## 执行安装配置清单中的Office产品
setup /configure configuration-2019.xml
~~~

## 制作镜像包，方便以后安装
* 在当前路径下，使用`Bandzip`压缩，格式选择`ISO`
* 测试镜像安装：卸载本地安装的Office、重启电脑、双击镜像文件，双击install.bat

## 激活
参考：https://github.com/massgravel/Microsoft-Activation-Scripts

## 感谢
* https://www.cnblogs.com/sysin/p/15324207.html