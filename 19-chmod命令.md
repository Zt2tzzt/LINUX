# chmod 命令

## 一、chmod 命令修改权限

chmod 命令，可修改文件、文件夹的所属权限信息。

注意，只有文件、文件夹的所属用户，或 root 用户可以修改。

语法：`chmod [-R] 权限 文件或文件夹`

- `-R` 选项，可选，表示对文件夹内的全部内容应用同样的操作，不写，则表示仅用于文件夹本身。

将当前工作目录的 abc.txt 文件权限，修改为 rwxr-x--x：

```shell
chmod u=rwx,g=rx,o=x abc.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# chmod u=rwx,g=rx,o=x abc.txt
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# ls -l abc.txt
-rwxr-x--x 1 root root 126 3月   2 20:56 abc.txt
```

其中：u 表示 user 所属用户权限，g 表示 group 组权限，o 表示 other 其它用户权限.

将当前工作目录下，文件夹 haha 以及文件夹内全部内容权限设置为：rwxr-x--x

```shell
chmod -R u=rwx,g=rx,o=x haha
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# chmod -R u=rwx,g=rx,o=x haha
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# ls -l haha
总用量 4
-rwxr-x--x 1 root root 27 2月  29 16:10 test.txt
```

> ls 命令输出的显眼的文件夹颜色，在 Linux 中，通常表示危险的文件夹。

## 二、数字序号标记权限

权限可以用 3 位数字来代表，第一位数字表示用户权限，第二位表示用户组权限，第三位表示其它用户权限。

数字的细节如下：r 记为 4，w 记为 2，x 记为 1，

可以有：

- `0`：无任何权限，即 ---
- `1`：仅有 x 权限，即 --x
- `2`：仅有 w 权限，即 -w-
- `3`：有 w 和 x 权限，即 -wx
- `4`：仅有 r 权限，即 r--
- `5`：有 r 和 x 权限，即 r-x
- `6`：有 r 和 w 权限，即 rw-
- `7`：有全部权限，即 rwx

举例：命令 `chmod 751 hello.txt`，将 hello.txt 的权限修改为 751，rwx(7)，r-x(5)，--x(1)

将 abc.txt 的权限修改为： r-x--xr-x

```shell
chmod 515 abc.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# chmod 515 abc.txt
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]#  ls -l abc.txt
-r-x--xr-x 1 root root 126 3月   2 20:56 abc.txt
```

将 abc.txt 的权限修改为： -wx-w-rw-

```shell
chmod 326 abc.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]# chmod 326 abc.txt
[root@iZwz9clzmhmmlb65bbcvuuZ zetian]#  ls -l abc.txt
--wx-w-rw- 1 root root 126 3月   2 20:56 abc.txt
```

序号123代表的权限是：

`--x-w--wx`
