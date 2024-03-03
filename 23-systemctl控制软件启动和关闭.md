# systemctl 控制软件启动和关闭

Linux 系统很多软件（内置或第三方）均支持使用 systemctl 命令管理软件服务的启动、停止、开机自启。

systemctl 命令能够管理的软件，一般也称之为：服务

语法：`systemctl start | stop | status | enable | disable 服务名`

- `start`，表示启动。
- `stop`，表示停止。
- `status`，表示查看状态。
- `enable`，表示开启开机启动。
- `disable`，表示关闭开机启动。

系统内置的服务比较多，比如：

- NetworkManager，主网络服务。
- network，副网络服务。
- firewalld，防火墙服务。
- sshd，ssh 服务（FinalShell 远程登录 Linux 使用的就是这个服务）

## 一、系统软件服务

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

## 二、第三方软件服务

除了系统内置的服务以外，部分第三方软件安装后，自行在系统中注册了服务，也可以用 systemctl 进行控制。

比如 ntp 软件的 ntpd 服务

安装 ntp 软件

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

比如 apache 服务器软件的 httpd 软件的 httpd 服务

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
