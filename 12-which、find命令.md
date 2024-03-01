# which、find 命令

## 一、which 命令

在前面学习的 Linux 命令，其实它们的本体，就是一个个的二进制可执行程序（就像 Windows 系统中的 .exe 文件）。

可以通过 which 命令，查看所使用的命令的程序文件存放位置。

语法：`which 要查找的命令`

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# which cd
/usr/bin/cd
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# which pwd
/usr/bin/pwd
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# which touch
/usr/bin/touch
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# which mkdir
/usr/bin/mkdir
```

## 二、find 命令

在 Windows、Mac 的图形化界面中，可以方便的通过系统提供的搜索功能，搜索指定的文件。

在 Linux 系统中，需要通过 find 命令去搜索指定的文件。

### 1.查找指定文件名

语法：`find 起始路径 -name "被查找的文件名"`

示例：从根目录开始搜索，查找文件名为 test 的文件：

```shell
find / -name "test"
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# find / -name "test"
/usr/src/kernels/3.10.0-1160.105.1.el7.x86_64/include/config/test
/usr/src/kernels/3.10.0-1160.105.1.el7.x86_64/drivers/ntb/test
/usr/src/kernels/3.10.0-1160.105.1.el7.x86_64/lib/raid6/test
/usr/lib/modules/3.10.0-1160.el7.x86_64/kernel/drivers/ntb/test
/usr/lib/modules/3.10.0-1160.105.1.el7.x86_64/kernel/drivers/ntb/test
/usr/lib64/python3.6/test
/usr/lib64/python2.7/test
/usr/lib64/python2.7/unittest/test
/usr/bin/test
```

### 2.通配符的使用

被查找文件名，支持使用通配符 * 来做模糊查询。

符号 `*` 表示通配符，即匹配任意内容（包含空）

- `test*`，表示匹配任何以 test 开头的内容。
- `*test`，表示匹配任何以 test 结尾的内容。
- `*test*`，表示匹配任何包含 test 的内容。

基于通配符的含义，可以结合 find 命令做文件的模糊查询：

查找所有以 test 开头的文件

```shell
find / -name “test*”
```

查找所有以 test 结尾的文件：

```shell
find / -name “*test”
```

查找所有包含 test 的文件：

```shell
find / -name “*test*”
```

### 3.查找指定大小的文件

find 命令，按照文件大小，查找文件。

语法：`find 起始路径 -size +|-n[kMG]`

- `+`、`-` 分别表示大于、小于。
- `n` 表示数字。
- `kMG` 表示大小单位，`k`（小写字母）表示 kb，`M` 表示 MB，`G` 表示 GB

查找小于 10KB 的文件：

```shell
find / -size -10k
```

查找大于 100MB 的文件：

```shell
find / -size +100M
```

查找大于1GB的文件：

```shell
find / -size +1G
```

## 三、练习

使用 find 命令找出：名称中带有 centos 的文件

```shell
find / -name "*centos*"
```

使用 find 命令找出：/usr 目录内大于 100M 的文件

```shell
find /usr -size +100M
```
