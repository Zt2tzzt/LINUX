# grep、wc 命令和管道符

## 一、grep 命令

可以通过 grep 命令，从文件中通过关键字过滤文件行。

语法：`grep [-n] "关键字" 文件路径`

- `-n` 选项，可选，表示在结果中显示匹配的行的行号。
- `"关键字"`，必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用双引号（””）将关键字包围起来。
- `文件路径`，必填，表示要过滤内容的文件的路径，可作为内容输入端口。

现在，通过 touch 命令在 ZeTianShop 目录创建文件 zetian.txt，然后使用图形化界面编辑并保存如下内容：

```txt
zetian is a employee of kkcf
kkcf full name is KunKunChickenFarm
```

在 zetian.txt 中，过滤 “zetian” 关键字

```shell
grep "zetian" zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# grep "zetian" zetian.txt
zetian is a employee of kkcf
```

在 zetian.txt 中，过滤 “kkcf” 关键字

```shell
grep "kkcf" zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# grep "kkcf" zetian.txt
zetian is a employee of kkcf
kkcf full name is KunKunChickenFarm
```

在 zetian.txt 中，过滤 “full” 关键字，并显示行号

```shell
grep -n "full" zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# grep -n "full" zetian.txt
2:kkcf full name is KunKunChickenFarm
```

## 二、wc 命令

通过 `wc` 命令统计文件的行数、单词数量，字节数，字符数等.

语法：`wc [-c -m -l -w] 文件路径`

- `-l` 选项，统计行数。
- `-w` 选项，统计单词数量。
- `-c` 选项，统计 bytes 数量。
- `-m` 选项，统计字符数量。
- `文件路径` 参数，被统计的文件，可作为内容输入端口。

不加选项：统计文件

```shell
wc zetian.txt
```

```shell
kkcf full name is KunKunChickenFarm[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]#
 1 11 61 zetian.txt
```

展示的信息依次是：行数，单词数，字节数，文件名

统计字节数

```shell
wc -c zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# wc -c zetian.txt
61 zetian.txt
```

统计字符数

```shell
wc -m zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# wc -m zetian.txt
61 zetian.txt
```

统计行数

```shell
wc -l zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# wc -l zetian.txt
1 zetian.txt
```

统计单词数

```shell
wc -w zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# wc -w zetian.txt
11 zetian.txt
```

## 三、管道符

管道符的含义是：将管道符左边命令的结果，作为右边命令的输入。

将 `cat zetian.txt` 的输出结果（文件内容），作为右边 grep 命令的输入（被过滤文件）

```shell
cat zetian.txt | grep "kkcf"
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat zetian.txt | grep "kkcf"
zetian is a staff of kkcf
kkcf full name is KunKunChickenFarm
```

将 `cat zetikan.txt` 的输出结果（文件内容），作为右边 wc 命令的输入（被统计的文件）

```shell
cat zetian.txt | wc -l
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat zetian.txt | wc -l
1
```

只要能产生内容输出的命令，都可以结合管道符使用

将 `ls` 的输出结果（当前目录下内容），作为右边 grep 命令的输入（被过滤的内容）

```shell
ls | grep "test"
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# ls
haha  test3  test4  zetian.txt
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# ls | grep "test"
test3
test4
```

```shell
ls -l /usr/bin | grep "Mail"
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# ls -l /usr/bin | grep "Mail"
lrwxrwxrwx  1 root root        15 1月  25 10:27 Mail -> ../../bin/mailx
```

将 `ls -l /usr/bin` 的输出结果（当前目录下内容），作为右边 wc 命令的输入（被统计的行数）

```shell
ls -l /usr/bin | wc -l
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# ls -l /usr/bin | wc -l
813
```

将 `cat zetian.txt` 的输出结果（文件内容），作为右边 grep 命令的输入（被过滤文件），再作为右边 grep 命令的输入（被过滤的文件）

管道符的嵌套使用。

```shell
cat zetian.txt | grep "kkcf" | grep "KunKunChickenFarm"
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cat zetian.txt | grep "kkcf" | grep "KunKunChickenFarm"
kkcf full name is KunKunChickenFarm
```

## 三、练习

对创建的 zetian.txt 进行统计。

要求使用 cat、grep、wc 命令、管道符，进行统计：

统计文件中带有 KunKunChickenFarm 关键字的有几行：

```shell
cat zetian.txt | grep "KunKunChickenFarm" | wc -l
```

统计文件中带有 kkcf 关键字的结果中有多少个单词：

```shell
cat zetian.txt | grep "kkcf" | wc -w
```
