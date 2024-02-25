# Windows 配置 WSL

## 一、WSL 为什么要用？

WSL 作为 Windows 系统带来的全新特性，正在逐步颠覆开发人员既有的选择。

传统方式获取 Linux 操作系统环境，是安装完整的虚拟机，如 VMware；

使用 WSL，可以以非常轻量化的方式，得到 Linux 系统环境。

目前，开发者正在逐步抛弃以虚拟机的形式获取 Linux 系统环境，而在逐步拥抱 WSL 环境。

## 二、WSL 是什么？

WSL（Windows Subsystem for Linux）是用于 Windows 系统之上的 Linux 子系统。

作用很简单，可以在 Windows 系统中获得 Linux 系统环境，并完全直连计算机硬件，无需通过虚拟机虚拟硬件。且不会影响Windows 系统本身的运行

![WSL](/Users/zetian/workshop/tutorial/LINUX/NoteAssets/WSL.png)

## 三、WSL 开启

WSL 是 Windows10 自带功能，需要开启，无需下载

打开系统的“启用或关闭 Windows 功能”，勾选“适用于 Linux 的 Windows 子系统”。

然后重启电脑。

在 Microsoft 应用商店，搜索“Ubuntu”，选择第一个安装。

## 四、WSL 中安装 Ubuntu 发行版

点击下载好的 Ubuntu 启动。

输入用户名，用以创建一个用户 `zetian`。

输入两次密码确认 `123456`（输入的密码没有反馈）。

至此，得到了一个可用的 Ubuntu 操作环境。

---

Ubuntu 自带的终端窗口软件不太好用，可以使用微软推出的：Windows Terminal 软件

在应用商店中搜索 terminal 关键字，找到 Windows Terminal 软件下载并安装。

在 Windows Termina 中，设置默认代开 Ubuntu。
