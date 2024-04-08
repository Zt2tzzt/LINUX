# systemctl 控制软件启动和关闭

`systemd` 是 Linux 系统的一种初始化系统（init system），也是一种服务管理框架。

许多 Linux 发行版都采用了 `systemd`，并使用其中的 `systemctl` 命令来管理系统服务。很多第三方软件，也支持使用 `systemctl` 命令，管理软件服务的启动、停止、开机自启等等状态。

`systemctl` 命令能够管理的软件，一般也称之为：服务。

语法：`systemctl start | stop | status | enable | disable 服务名`

- `start`，表示启动。
- `stop`，表示停止。
- `status`，表示查看状态。
- `enable`，表示开启开机启动。
- `disable`，表示关闭开机启动。

## 一、systemctl 命令和 service 命令

在 Linux 系统中，`systemctl` 命令和 `service` 命令的

相似之处：

1. **管理服务**：`systemctl` 命令和 `service` 命令都用于管理系统服务。
2. **启动服务**：两者都可以用来启动特定服务。
3. **停止服务**：都可以用来停止特定服务。
4. **重启服务**：两者都可以用来重新启动特定服务。
5. **查看服务状态**：都可以查看当前正在运行的服务的状态。

不同之处：

1. **系统支持**：`systemctl` 命令通常用于最新的 `systemd` 初始化系统，而 `service` 命令是传统 `SysV` 初始化系统中使用的命令。
2. **功能丰富性**：`systemctl` 提供了更多功能，例如可以控制系统引导和管理系统单元等。
3. **语法**：`systemctl` 命令的语法比 `service` 命令更为一致和简单。
4. **可读性**：`systemctl` 输出信息更加易于阅读和理解。

适用场景：

- **`systemctl` 适用场景**：
  - 用于 `systemd` 初始化系统的 Linux 发行版，如 CentOS 7、Ubuntu 16.04 及更高版本等。
  - 适用于管理系统服务、查看和控制单元的状态等。
  - 更加强大且现代的服务管理工具，提供更多的功能和选项。
- **`service` 适用场景**：
  - 在传统的 `SysV` 初始化系统中，如 Ubuntu 14.04 及更低版本等。
  - 用于基本的服务管理，如启动、停止和重新启动服务。
  - 更适合于旧版本的 Linux 系统或仍在使用 `SysV` 初始化系统的服务器环境。

总的来说，`systemctl` 是更现代、功能更丰富、更易用的服务管理工具，而 `service` 则是更传统、简单的服务管理命令。根据您的Linux 发行版和初始化系统，您可以选择适合您环境的命令来管理和控制服务。

systemctl 命令和 service 命令常用命令分别有哪些？

`systemctl` 常用命令：

1. **启动服务**：`systemctl start <service>`
2. **停止服务**：`systemctl stop <service>`
3. **重新启动服务**：`systemctl restart <service>`
4. **查看服务状态**：`systemctl status <service>`
5. **启用开机自启**：`systemctl enable <service>`
6. **禁用开机自启**：`systemctl disable <service>`
7. **查看所有正在运行的服务**：`systemctl list-units --type=service`
8. **查看特定服务的配置文件**：`systemctl cat <service>`
9. **查看服务的日志**：`journalctl -u <service>`
10. **查看启动失败的服务**：`systemctl --failed`

`service` 常用命令：

1. **启动服务**：`service <service> start`
2. **停止服务**：`service <service> stop`
3. **重新启动服务**：`service <service> restart`
4. **查看服务状态**：`service <service> status`
5. **启用开机自启**：`chkconfig <service> on`
6. **禁用开机自启**：`chkconfig <service> off`
7. **查看开机启动状态**：`chkconfig --list`

`systemctl` 提供了更加一致和直观的命令语法，而`service`更侧重于传统 `SysV` 初始化系统的命令风格。根据您的系统使用 `systemd` 还是 `SysV` 初始化系统，选择适合的命令进行服务管理。

## 二、系统软件服务

Linux 系统有很多内置的服务，比如：

- NetworkManager，主网络服务。
- network，副网络服务。
- firewalld，防火墙服务。
- sshd，ssh 服务（FinalShell 远程登录 Linux 使用的就是这个服务）。

> d 是 daemon，表示进程。

使用 `systemctl` 命令，开启 firewalld 服务。

```shell
systemctl start firewalld
```

使用 `systemctl` 命令，停止 firewalld 服务。

```shell
systemctl stop firewalld
```

使用 `systemctl` 命令，查看 firewalld 服务状态。

```shell
systemctl status firewalld
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# systemctl status firewalld
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
   Active: inactive (dead)
     Docs: man:firewalld(1)
```

## 三、第三方软件服务

除了系统内置的服务以外，部分第三方软件安装后，自行在系统中注册了服务，也可以用 systemctl 进行控制。

比如 ntp 软件的 ntpd 服务

安装 ntp 软件：

```shell
yum -y install ntp
```

然后使用 systemctl 命令，开启 ntpd 服务

```shell
systemctl start ntpd
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# systemctl start ntpd
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# systemctl status ntpd
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; disabled; vendor preset: disabled)
   Active: active (running) since 日 2024-03-03 20:58:15 CST; 8s ago
  Process: 16732 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 16733 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─16733 /usr/sbin/ntpd -u ntp:ntp -g

3月 03 20:58:15 iZwz9clzmhmmlb65bbcvuuZ systemd[1]: Starting Network Time Service...
3月 03 20:58:15 iZwz9clzmhmmlb65bbcvuuZ systemd[1]: Started Network Time Service.
3月 03 20:58:15 iZwz9clzmhmmlb65bbcvuuZ ntpd[16733]: proto: precision = 0.043 usec
3月 03 20:58:15 iZwz9clzmhmmlb65bbcvuuZ ntpd[16733]: 0.0.0.0 c01d 0d kern kernel time sync enabled
```

比如 apache 服务器的 httpd 软件的 httpd 服务

安装 httpd 软件

```shell
yum -y install httpd
```

然后使用 systemctl 命令，开启 httpd 服务

```shell
systemctl start httpd
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# systemctl start httpd
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since 日 2024-03-03 21:02:11 CST; 3s ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 21235 (httpd)
   Status: "Processing requests..."
   CGroup: /system.slice/httpd.service
           ├─21235 /usr/sbin/httpd -DFOREGROUND
           ├─21236 /usr/sbin/httpd -DFOREGROUND
           ├─21237 /usr/sbin/httpd -DFOREGROUND
           ├─21238 /usr/sbin/httpd -DFOREGROUND
           ├─21239 /usr/sbin/httpd -DFOREGROUND
           └─21240 /usr/sbin/httpd -DFOREGROUND

3月 03 21:02:11 iZwz9clzmhmmlb65bbcvuuZ systemd[1]: Starting The Apache HTTP Server...
3月 03 21:02:11 iZwz9clzmhmmlb65bbcvuuZ httpd[21235]: AH00558: httpd: Could not reliably determine the server's fully q...ssage
3月 03 21:02:11 iZwz9clzmhmmlb65bbcvuuZ systemd[1]: Started The Apache HTTP Server.
Hint: Some lines were ellipsized, use -l to show in full.
```

> 系统内置服务均可被 systemctl 管理。
>
> 安装的第三方软件，只要能自行在系统中注册服务的，就可以使用 systemctl 管理。
>
> 事实上，部分软件安装后，没有自动在系统中注册服务，需要手动注册后，才能使用 systemctl 管理。

## 四、WSL 中的替代方案

有些老版本的 WSL 由于其特殊性并不使用 `systemd`。所以也没有使用 `systemd` 来管理系统服务。

目前，解决这个问题有下面一些流行的方法：

① **升级到 WSL 2 并手动启动 systemd**

最新版的 WSL 2 已经支持 `systemd` 服务，将 WSL 升级为最新的版本。

```shell
wsl --update
```

① **直接使用 service 命令来管理服务**

比如对于 MySQL，你可以使用 `service` 命令来启动和停止服务，而不是 `systemctl`：

```bash
sudo service mysql start
sudo service mysql stop
sudo service mysql status
```
