# Nginx 安装部署【简单】

## 一、Nginx 介绍

_Nginx_ 是一个高性能的 HTTP 和反向代理 web 服务器，同时也提供了 IMAP/POP3/SMTP 服务。

同 Tomcat 一样，Nginx 可以托管用户编写的 WEB 应用程序成为可访问的网页服务；同时也可以作为流量代理服务器，控制流量的中转。

Nginx 在 WEB 开发领域，基本上也是必备组件之一了。

## 二、Nginx 安装

### 1.CentOS 安装

Nginx 同样需要配置额外的 yum 仓库，才可以使用 yum 安装

> 安装 Nginx 的操作需要 root 身份

1️⃣ 安装 yum 依赖程序

```shell
# root执行
yum install -y yum-utils
```

2️⃣ 手动添加，nginx 的 yum 仓库

yum 程序使用的仓库配置文件，存放在：/etc/yum.repo.d 内。

```shell
# root执行
# 创建文件使用vim编辑
vim /etc/yum.repos.d/nginx.repo
```

/etc/yum.repos.d/nginx.repo

```shell
# 填入如下内容并保存退出
[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true

[nginx-mainline]
name=nginx mainline repo
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
gpgcheck=1
enabled=0
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
```

> 通过如上操作，我们手动添加了 nginx 的 yum 仓库

3️⃣ 通过 yum 安装最新稳定版的 nginx

```shell
# root执行
yum install -y nginx
```

4️⃣ 启动

```shell
# nginx自动注册了systemctl系统服务
systemctl start nginx # 启动
systemctl stop nginx # 停止
systemctl status nginx # 运行状态
systemctl enable nginx # 开机自启
systemctl disable nginx # 关闭开机自启
```

5️⃣ 配置防火墙放行

nginx 默认绑定 80 端口，需要关闭防火墙或放行 80 端口

```shell
# 方式1（推荐），关闭防火墙
systemctl stop firewalld # 关闭
systemctl disable firewalld # 关闭开机自启

# 方式2，放行 80 端口
firewall-cmd --add-port=80/tcp --permanent # 放行tcp规则下的80端口，永久生效
firewall-cmd --reload # 重新加载防火墙规则
```

6️⃣ 启动后浏览器输入 Linux 服务器的 IP 地址或主机名即可访问

`http://ip地址` 或 `http://主机名`

> ps：80 端口是访问网站的默认端口，所以后面无需跟随端口号

至此，Nginx 安装配置完成。

![image-20221018143113053](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/18/20221018143113.png)

### 2.Ubuntu 安装

在 Ubuntu 系统中，可以通过以下步骤来安装 `nginx`：

① 打开一个终端窗口

② 首先，更新你的包索引以使其获取到最新的关于软件和它们版本的信息：

```bash
sudo apt update
```

安装 `nginx`：

```bash
sudo apt install nginx
```

⑦ 安装 `nginx` 之后，它应该会被自动启动。你可以通过如下命令来确认 `nginx` 是否正在运行：

```bash
systemctl status nginx
```

如果 `nginx` 成功运行，你应该能看到 `active (running)` 在输出的文本中。
