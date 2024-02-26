# cp、mv、rm 命令

## 一、cp 命令

cp 命令来自英文单词：copy。可以用于复制文件 \ 文件夹

语法：`cp [-r] [参数一] [参数二]`

- `-r` 选项，可选，用于复制文件夹使用，表示递归。
- `参数1`，Linux 路径，表示被复制的文件或文件夹。
- `参数2`，Linux 路径，表示要复制去的地方。

将当前工作目录的 test.txt 复制为 text2.txt

```shell
cp test.txt test2.txt
```

复制当前工作目录的 test1 文件夹。发现有“略过目录”的提示。

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cp test1 test4
cp: 略过目录"test1"
```

复制文件夹，必须使用-r选项，否则不会生效。

```shell
cp -r test1 test11
```

## 二、mv 命令

mv 命令，来自英文单词：move；可以用于移动文件 \ 文件夹。

语法：`mv [参数一] [参数二]`

- `[参数1]`，Linux 路径，表示被移动的文件或文件夹
- `[参数2]`，Linux 路径，表示要移动去的地方，如果目标不存在，则进行重命名。

在当前工作目录，移动 test1.txt 文件，到 test1 文件夹中。

```shell
mv test.txt test1
```

将 test2.txt 文件改名为 test3.txt 文件。

```shell
mv test2.txt test3.txt
```

将 test11 文件夹，移动到 test1 文件夹里

```shell
 mv test11 test1
```

## 三、rm 命令

认识到的第一个，支持无限数量参数的命令



删除文件



删除文件夹



一次性删除多个目标。



rm 命令结合通配符。



rm 的 -f 选项。

> exit 命令，从 root 用户退回到普通用户。