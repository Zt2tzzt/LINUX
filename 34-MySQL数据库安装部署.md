# MySQL 数据库安装部署【简单】

## 一、MySQL 简介

MySQL 数据库管理系统（后续简称 MySQL），是一款知名的数据库系统，其特点是：轻量、简单、功能丰富。

MySQL 数据库可谓是软件行业的明星产品，无论是后端开发、大数据、AI、运维、测试等各类岗位，基本上都会和 MySQL 打交道。

## 二、MySQL5.7 在 CentOS 中安装

==安装操作需要 root 权限==

1️⃣ MySQL 并不在 CentOS 的官方仓库中，要通过 rpm 命令：

- 导入 MySQL 仓库的密钥；
- 配置 MySQL 的 yum 仓库；

```shell
# 更新密钥
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022

# 安装 Mysql yum 库
rpm -Uvh http://repo.mysql.com//mysql57-community-release-el7-7.noarch.rpm
```

![image-20221012182514865](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012182514.png)

2️⃣ 使用 yum 安装 MySQL

```shell
# yum安装Mysql
yum -y install mysql-community-server
```

![image-20221012182555420](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012182556.png)

MySQL安装完成后，会自动配置为名称叫做：`mysqld` 的服务，可以被 systemctl 所管理

4️⃣ 启动 MySQL 服务，并配置开机自启动

```shell
systemctl start mysqld # 启动
systemctl enable mysqld # 开机自启
```

5️⃣ 检查 MySQL 的运行状态

```shell
systemctl status mysqld
```

![image-20221012182716598](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012182716.png)

## 三、MySQL5.7 在 CentOS 中配置

主要配置管理员用户 root 的密码，以及配置允许远程登录的权限。

1️⃣ 获取 MySQL 的初始密码。

通过 grep 命令，在/var/log/mysqld.log 文件中，过滤 temporary password 关键字，得到初始密码

```shell
grep 'temporary password' /var/log/mysqld.log
```

![image-20221012182744115](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012182744.png)

2️⃣ 登陆MySQL数据库系统

```shell
# 执行
mysql -uroot -p
```

-u，登陆的用户，MySQL数据库的管理员用户同 Linux 一样，是 root。

-p，表示使用密码登陆。

执行完毕后输入刚刚得到的初始密码，即可进入 MySQL 数据库

![image-20221012182805966](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012182806.png)

3️⃣ 修改 root 用户密码

在 MySQL 控制台内执行 SQL 语句。

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '密码 -- 密码需要符合：大于8位，有大写字母，有特殊符号，不能是连续的简单语句如123，abc
```

[扩展]，配置 root 用户的简单密码

> 在学习阶段，可以给 root 设置简单密码，如 123456.

执行如下 SQL 语句：

```sql
set global validate_password_policy=LOW; # 密码安全级别低
set global validate_password_length=4; # 密码长度最低4位即可

# 设置简单密码
ALTER USER 'root'@'localhost' IDENTIFIED BY '简单密码';
```

[扩展]，配置 root 运行远程登录

默认情况下，root 用户是不运行远程登录的，只允许在本地登陆 MySQL 系统。

> 请注意，允许 root 远程登录会带来安全风险

```sql
# 授权root远程登录
grant all privileges on *.* to root@"IP地址" identified by '密码' with grant option;
# IP 地址即允许登陆的IP地址，也可以填写 %，表示允许任何地址
# 密码表示给远程登录独立设置密码，和本地登陆的密码可以不同

# 刷新权限，生效
flush privileges;
```

退出MySQL控制台页面

```sql
# 退出命令
exit

# 或者通过快捷键退出：ctrl + d
```

4️⃣ 检查端口

MySQL 默认绑定了 3306 端口，可以通过端口占用检查 MySQL 的网络状态。

```shell
netstat -anp | grep 3306
```

![image-20221012183746802](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012183746.png)

至此，MySQL 就安装完成并可用了，请妥善保存好 MySQL 的 root 密码。

## 四、MySQL8.0 在 CentOS 中安装

==注意：安装操作需要root权限==

与 MySQL 5.7 相比，在 root 用户配置，和远程登录配置上有所不同。

> `rpm` 是 Red Hat 包管理器，可以用于安装、卸载、升级、查询和验证软件包。

1️⃣ 配置 yum 仓库

```shell
# 更新密钥
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql
```

打开 [http://dev.mysql.com/downloads/repo/yum/](https://link.zhihu.com/?target=http%3A//dev.mysql.com/downloads/repo/yum/)

根据你的系统版本，选择对应的安装包，

例如我的系统发行版是 CentOS 7.9，这个发行版的 Linux 内核是 Linux 7，所以我选择了红框内的地址。

![rpm 安装包](https://pic1.zhimg.com/80/v2-c7386b38916fc9958490b651a93d0860_720w.jpg)

2️⃣ 安装 MySQL8.x 版本 yum 库。

拿到安装包，在前面拼接 `http://dev.mysql.com/get/`

然后使用 rpm，安装 MySQL 的 yum 库。

```shell
rpm -Uvh http://dev.mysql.com/get/mysql80-community-release-el7-11.noarch.rpm
```

使用 yum 安装MySQL

```shell
yum -y install mysql-community-server
```

3️⃣ 安装完成后，启动 MySQL 并配置开机自启动

MySQL 安装完成后，会自动配置为名称叫做：`mysqld` 的服务，可以被 systemctl 所管理

```shell
systemctl start mysqld« # 启动
systemctl enable mysqld # 开机自启
```

检查 MySQL 的运行状态

```shell
systemctl status mysqld
```

## 五、MySQL 8.0 在 CentOS 中配置

主要修改 root 密码和允许 root 远程登录

1️⃣ 获取 MySQL 的初始密码

```shell
# 通过 grep 命令，在 /var/log/mysqld.log 文件中，过滤 temporary password 关键字，得到初始密码
grep 'temporary password' /var/log/mysqld.log
```

2️⃣ 登录 MySQL 数据库系统

```shell
# 执行
mysql -uroot -p

# 解释
# -u，登陆的用户，MySQL数据库的管理员用户同Linux一样，是root
# -p，表示使用密码登陆

# 执行完毕后输入刚刚得到的初始密码，即可进入MySQL数据库
```

3️⃣ 修改 root 密码

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '密码'; -- 密码需要符合：大于8位，有大写字母，有特殊符号，不能是连续的简单语句如123，abc
```

[扩展]：配置 root 的简单密码

> 可以给 root 设置简单密码，如 123456.
>
> 请注意，此配置仅仅用于学习 的MySQL

执行如下 Sql 语句：

```sql
set global validate_password.policy=0; # 密码安全级别低
set global validate_password.length=4; # 密码长度最低4位即可
```

[扩展]：允许 root 远程登录，并设置远程登录密码

> 默认情况下，root 用户是不运行远程登录的，只允许在本地登陆 MySQL 系统。
>
> 请注意，允许 root 远程登录会带来安全风险。

执行如下 Sql 语句：

```sql
# 第一次设置 root 远程登录，并配置远程密码使用如下SQL命令
create user 'root'@'%' IDENTIFIED WITH mysql_native_password BY '密码!'; -- 密码需要符合：大于8位，有大写字母，有特殊符号，不能是连续的简单语句如123，abc

# 后续修改密码使用如下 SQL 命令
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '密码';
```

4️⃣ 退出MySQL控制台页面

```sql
# 退出命令
exit

# 或者通过快捷键退出：ctrl + d
```

5️⃣ 检查端口

MySQL 默认绑定了 3306 端口，可以通过端口占用检查 MySQL 的网络状态

```shell
netstat -anp | grep 3306
```

![image-20221012192303607](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/12/20221012192303.png)

至此，MySQL就安装完成并可用了，请妥善保存好 MySQL 的 root 密码。

## 六、MySQL5.7 在 Ubuntu 中安装和配置

> WSL 环境是最新的 Ubuntu22.04 版本，这个版本的软件商店内置的 MySQL 是 8.0 版本
>
> 所以需要额外的步骤才可以安装 5.7 版本的 MySQL

==安装操作需 root 权限==，你可以：

- 通过 sudo su -，切换到 root 用户。
- 或在每一个命令前，加上 sudo，用来临时提升权限。

1️⃣ 下载 apt 仓库文件

```shell
# 下载 apt 仓库的安装包，Ubuntu 的安装包是 .deb 文件
wget https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb
```

![image-20221016094103315](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094103.png)

2️⃣ 配置 apt 仓库

```shell
# 使用 dpkg 命令安装仓库
dpkg -i mysql-apt-config_0.8.12-1_all.deb
```

弹出框中选择：`ubuntu bionic` （Ubuntu18.04 系统的代号是 bionic，选择 18.04 的版本库用来安装）

![image-20221016094142343](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094142.png)

弹出框中选择：`MySQL Server & Cluster`

![image-20221016094216377](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094216.png)

弹出框中选择：`mysql-5.7`

![image-20221016094254397](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094254.png)

最后选择：`ok`

![image-20221016094306917](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094306.png)

3️⃣ 更新 apt 仓库的信息

```shell
# 首先导入仓库的密钥信息
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 467B942D3A79BD29
# 更新仓库信息
apt update
```

4️⃣ 检查是否成功配置 MySQL5.7 的仓库

```shell
apt-cache policy mysql-server
```

![image-20221016094546943](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094546.png)

看到如图所示字样，即成功

5️⃣ 安装 MySQL5.7

```shell
# 使用apt安装mysql客户端和mysql服务端
apt install -f -y mysql-client=5.7* mysql-community-server=5.7*
```

弹出框中输入 root 密码并选择 ok，密码任意，比如 123456

![image-20221016094941439](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094941.png)

再次输入 root 密码确认

![image-20221016094954505](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016094954.png)

6️⃣ 启动 MySQL

MySql 5.7 没有注册 systemctl 的服务。

所以要手动的启动它。

```shell
/etc/init.d/mysql start # 启动
/etc/init.d/mysql stop # 停止
/etc/init.d/mysql status # 查看状态
```

![image-20221016095259172](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095259.png)

7️⃣ 对 MySQL 进行初始化

```shell
# 执行如下命令，此命令是MySQL安装后自带的配置程序
mysql_secure_installation

# 可以通过which命令查看到这个自带程序所在的位置
root@DESKTOP-Q89USRE:~# which mysql_secure_installation
/usr/bin/mysql_secure_installation
```

① 输入密码：

![image-20221016095458755](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095458.png)

② 是否开启密码验证插件，如果需要增强密码安全性，输入`y`并回车，不需要直接回车（案例中中选择直接回车）

![image-20221016095537716](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095537.png)

③ 是否更改root密码，需要输入`y`回车，不需要直接回车（案例中不更改）

![image-20221016095621386](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095621.png)

④ 是否移除匿名用户，移除输入`y`回车，不移除直接回车（案例中选择移除）

![image-20221016101232827](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101232.png)

⑤ 是否进制 root 用户远程登录，禁止输入`y`回车，不禁止直接回车（案例中选择不禁止）

![image-20221016101324577](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101324.png)

⑥ 是否移除自带的测试数据库，移除输入`y`回车，不移除直接回车（案例中选择不移除）

![image-20221016101404392](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101404.png)

⑦ 是否刷新权限，刷新输入`y`回车，不刷新直接回车（案例中选择刷新）

![image-20221016101442459](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101442.png)

8️⃣ 登陆 MySQL

```shell
mysql -uroot -p
# 输入密码即可登陆成功
```

![image-20221016101524498](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101524.png)

至此，在 Ubuntu 上安装 MySQL5.7 版本成功。

## 七、MySQL8.0 在 Ubuntu 中安装和配置

> WSL 环境是最新的 Ubuntu22.04 版本，这个版本的软件商店内置的 MySQL 是 8.0 版本
>
> 所以直接通过 apt 命令安装即可。

==安装操作需 root 权限==，你可以：

- 通过 sudo su -，切换到 root 用户。
- 或在每一个命令前，加上 sudo，用来临时提升权限。

1️⃣ 如果已经安装过 MySQL5.7 版本，需要卸载仓库信息

```shell
# 卸载 MySQL5.7 版本
apt remove -y mysql-client=5.7* mysql-community-server=5.7*

# 卸载 MySQL5.7 的仓库信息
dpkg -l | grep mysql | awk '{print $2}' | xargs dpkg -P
```

2️⃣ 更新 apt 仓库信息

```shell
apt update
```

3️⃣ 安装 mysql

```shell
apt install -y mysql-server
```

4️⃣ 启动 MySQL

```shell
/etc/init.d/mysql start # 启动
/etc/init.d/mysql stop # 停止
/etc/init.d/mysql status # 查看状态
```

5️⃣ 登陆 MySQL

```shell
# 直接执行：mysql
mysql
```

6️⃣ 设置密码，执行 SQL：

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

7️⃣ 退出 MySQL 控制台

```shell
exit
```

8️⃣ 对 MySQL 进行初始化

```shell
# 执行如下命令，此命令是 MySQL 安装后自带的配置程序
mysql_secure_installation

# 可以通过 which 命令查看到这个自带程序所在的位置
root@DESKTOP-Q89USRE:~# which mysql_secure_installation
/usr/bin/mysql_secure_installation
```

① 输入密码：

![image-20221016095458755](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095458.png)

② 是否开启密码验证插件，如果需要增强密码安全性，输入`y`并回车，不需要直接回车（案例中选择直接回车）

![image-20221016095537716](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095537.png)

③ 是否更改 root 密码，需要输入 `y` 回车，不需要直接回车（案例中不更改）

![image-20221016095621386](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016095621.png)

④ 是否移除匿名用户，移除输入`y`回车，不移除直接回车（案例中选择移除）

![image-20221016101232827](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101232.png)

⑤ 是否禁止 root 用户远程登录，禁止输入`y`回车，不禁止直接回车（案例中选择不禁止）

![image-20221016101324577](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101324.png)

⑥ 是否移除自带的测试数据库，移除输入`y`回车，不移除直接回车（案例中选择不移除）

![image-20221016101404392](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101404.png)

⑦ 是否刷新权限，刷新输入`y`回车，不刷新直接回车（案例中选择刷新）

![image-20221016101442459](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016101442.png)

9️⃣ 重新登陆 MySQL（用更改后的密码）

```shell
mysql -uroot -p
```

![image-20221016110414182](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/16/20221016110414.png)

至此，在 Ubuntu 上安装 MySQL8.0 版本成功。
