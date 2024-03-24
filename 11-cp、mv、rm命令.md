# cp、mv、rm 命令

## 一、cp 命令

cp 命令来自英文单词：copy。可以用于复制文件、文件夹

语法：`cp [-r] 参数一 参数二`

- `-r` 选项，可选，用于复制文件夹，表示递归。
- `参数1`，必填，Linux 路径，表示被复制的文件或文件夹。
- `参数2`，必填，Linux 路径，表示要复制去的地方。

### 1.复制文件

将当前工作目录的 test.txt 文件复制为 text2.txt 文件

```shell
cp test.txt test2.txt
```

### 2.复制文件夹（必须用 -r 选项）

将当前工作目录的 test1 文件夹复制为 test11 文件夹；

发现有“略过目录”的提示。

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# cp test1 test4
cp: 略过目录"test1"
```

cp 命令复制文件夹，必须使用 `-r` 选项，否则不会生效。

```shell
cp -r test1 test11
```

## 二、mv 命令

mv 命令，来自英文单词：move；可以用于移动文件、文件夹。

语法：`mv 参数一 参数]`

- `参数1`，必填，Linux 路径，表示被移动的文件或文件夹。
- `参数2`，必填，Linux 路径，表示要移动去的地方，如果目标不存在，则进行重命名。

### 1.移动文件、文件夹

在当前工作目录下，移动 test1.txt 文件，到 test1 文件夹中。

```shell
mv test.txt test1
```

在当前工作目录下，将 test11 文件夹，移动到 test1 文件夹里

```shell
mv test11 test1
```

### 2.重命名文件、文件夹

在当前工作目录下，将 test2.txt 文件改名为 test3.txt 文件。

```shell
mv test2.txt test3.txt
```

## 三、rm 命令

rm 命令来自英文单词：remove，可用于删除文件、文件夹。

rm 命令是目前认识到的第一个，支持无限数量参数的命令。

语法：`rm [-r -f] 参数1 [参数2] ... [参数n]`

- `-r` 选项，表示递归，用于删除文件夹。
- `-f` 选项表示 force，强制删除（不会弹出提示确认信息）。
  - 普通用户删除内容不会弹出提示，只有 root 超级管理员用户删除内容会有提示。
  - 所以一般普通用户用不到 `-f` 选项。
- `参数1 [参数2] ... [参数n]` 表示要删除的文件或文件夹路径，按照空格隔开语法：

### 1.删除文件

在当前工作目录下，删除文件 test.txt

```shell
rm test.txt
```

在当前工作目录下，一次性删除多个文件。

```shell
rm test1.txt test2.txt test3.txt
```

### 2.删除文件夹（必须用 -r 选项）

在当前工作目录下，删除 test1 文件夹：

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# rm test1
rm: 无法删除"test1": 是一个目录
```

rm 命令删除文件夹，必须使用 `-r` 选项

```shell
rm -r test1
```

> Linux 普通用户，切换到 root 用户
>
> 可以通过 `su - root`，并输入密码，临时切换到 root 用户体验。
>
> 输入 `exit` 命令，退回普通用户。
>

### 3.rm 命令和通配符

rm 命令支持通配符 `*`，用来做模糊匹配：

符号 `*` 表示通配符，即匹配任意内容（包含空）；

示例：

- `test*`，表示匹配任何以 test 开头的内容
- `*test`，表示匹配任何以 test 结尾的内容
- `*test*`，表示匹配任何包含 test 的内容

删除所有以 test 开头的文件 / 文件夹

````shell
rm -r test*
````

删除所有以 test 结尾的文件 / 文件夹

```shell
rm -r *test
```

删除所有包含 test 的内容

```shell
rm -r *test*
```

### 4.root 用户执行 rm 命令

rm 的 -f 选项的使用。

root 用户，在当前工作目录下，删除文件 test.txt，不让系统提示。

```shell
rm -f test.txt
```

root 用户，在当前工作目录下，删除文件夹 test1，不让系统提示。

```shell
rm -rf test1
```

### 4.rm 命令的危险

rm 是一个危险的命令，特别是在处于 root（超级管理员）用户的时候。请谨慎使用。

如下命令，请千万千万不要在 root 管理员用户下执行🤡：

`rm -rf /`

`rm -rf /*`
