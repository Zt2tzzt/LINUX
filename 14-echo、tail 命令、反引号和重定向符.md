# echo、tail 命令、反引号和重定向符

## 一、echo 命令

echo 命令，用于在命令行内输出指定内容。

语法：`echo 输出的内容`

无需选项，只有一个参数，表示要输出的内容，复杂内容（带有空格或 \ 等特殊符号），建议使用双引号包围可以用””包围，不然会影响命令的执行。

在终端上显示：Hello Linux

```shell
echo "Hello Linux"
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# echo "Hello Linux"
Hello Linux
```

## 二、反引号

被反引号 `` 包围的内容，会作为命令执行，而不是普通的字符。

```shell
echo `pwd`
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# echo `pwd`
/root/ZeTianShop
```

## 三、重定向符

重定向符：`>` 和 `>>`

`>`，将左侧命令的结果，覆盖写入到符号右侧指定的文件中。

`>>`，将左侧命令的结果，追加写入到符号右侧指定的文件中。

将 Hello Linux 写入岛当前工作目录的 zetian.txt 中，并覆盖其中的内容。

```shell
echo "Hello Linux" > zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# echo "Hello Linux" > zetian.txt
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat zetian.txt
Hello Linux
```

将 Hello KunKunChickenFarm 写入岛当前工作目录的 zetian.txt 中，并追加在最后面。

```shell
echo "Hello KunKunChickenFarm" >> zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# echo "Hello KunKunChickenFarm" >> zetian.txt
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat zetian.txt
Hello Linux
Hello KunKunChickenFarm
```

将 `ls -l` 命令输出的内容，写入到当前工作目录的 zetian.txt 中，并追加在最后面。

```shell
ls -l >> zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# ls -l >> zetian.txt
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat zetian.txt
Hello Linux
Hello KunKunChickenFarm
总用量 16
drwxr-xr-x 2 root root 4096 2月  27 20:48 haha
drwxr-xr-x 3 root root 4096 2月  25 17:17 test3
drwxr-xr-x 3 root root 4096 2月  27 20:46 test4
-rw-r--r-- 1 root root   36 2月  29 14:58 zetian.txt
```

## 四、tail 命令

tail 命令，用于查看文件尾部内容，跟踪文件的最新更改，

语法：`tail [-f -<num>] Linux路径`

- `-f` 选项，可选，表示持续跟踪。
- `-<num>` 选项，可选，表示查看尾部多少行，不填默认 10 行。
- `Linux路径`，参数，表示被跟踪的文件路径。

查看 /var/log/ecs_network_optimization.log 文件的尾部 10 行：

```shell
tail /var/log/ecs_network_optimization.log
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# tail /var/log/ecs_network_optimization.log
running /sbin/ecs_mq_rps_rfs
========  ECS network setting starts 2024-02-25 13:20:39 ========
optimize network performance: current device eth0
set and check multiqueue on eth0
only support 1 queue; no need to enable multiqueue on eth0
OK. irqbalance stoped.
max node :0
mask:1, irq:27
mask:2, irq:28
========  ECS network setting END 2024-02-25 13:20:39  ========
```

查看 /var/log/ecs_network_optimization.log 文件的尾部 3 行：

```shell
tail -3 /var/log/ecs_network_optimization.log
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# tail -3 /var/log/ecs_network_optimization.log
mask:1, irq:27
mask:2, irq:28
========  ECS network setting END 2024-02-25 13:20:39  ========
```

tail 命令跟踪文件变化：

使用 `-f` 选项，可以持续跟踪文件更改。

复制一个新的 FinalShell 的标签。

在第一个标签中，执行：`touch test.txt`，创建一个 test.txt 文件

在第一个标签中，执行：`tail -f test.txt`，持续跟踪文件更改

在第二个标签中，多次执行：`echo “内容” >> test.txt`，向文件追加内容

观察第一个标签的变化

## 五、练习

使用 echo 并配合反引号，输出内容：我当前的工作目录是：`具体的工作目录路径`，并结合重定向符，将输出结果覆盖写入work.txt文件

```shell
echo "我当前的工作目录是：`pwd`" >> work.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# echo "我当前的工作目录是：`pwd`" >> work.txt
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat work.txt
我当前的工作目录是：/root/ZeTianShop
```

使用 echo 输出任意内容，并追加到 work.txt 文件中；通过 tail 命令持续跟踪文件内容更改。

```shell
tail -f work.txt

echo "haha" >> work.txt
```
