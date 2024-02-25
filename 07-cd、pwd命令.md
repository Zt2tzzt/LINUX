# cd、pwd 命令

## 一、cd 命令

cd 切换工作目录

cd命令来自英文：Change Directory

普通用户的 Linux 命令行打开的时候，会默认以用户的 HOME 目录作为当前的工作目录

可以通过 cd 命令，更改当前所在的工作目录。

语法：`cd [Linux路径]`

cd 命令无需选项，只有参数，表示要切换到哪个目录下

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# cd /root/ZeTianShop/
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]#
```

cd 命令直接执行，不写参数，表示回到普通用户的 HOME 目录

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cd
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# pwd
/root
```

## 二、pwd 命令

pwd 查看当前工作目录

pwd 命令来自英文：Print Work Directory

语法：`pwd`

pwd 命令，无选项，无参数，直接输入 pwd 即可

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# pwd
/root
```

## 三、练习

使用 cd 命令并结合 ls 命令，任意在 Linux 文件系统内探索。

并尝试找出名字叫做 games 的文件夹在哪里。

参考答案：

/var/lib/games

/var/games

/usr/lib/games

/usr/lib64/games

/usr/share/games

/usr/games

/usr/local/games
