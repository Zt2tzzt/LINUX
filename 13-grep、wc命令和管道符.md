# grep、wc 命令和管道符

## 一、grep 命令

可以通过 grep 命令，从文件中通过关键字过滤文件行。

语法：`grep [-n] "关键字" 文件路径`

- `-n` 选项，可选，表示在结果中显示匹配的行的行号。
- `"关键字"`，必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用””将关键字包围起来。
- `文件路径`，必填，表示要过滤内容的文件的路径，可作为内容输入端口。

现在，通过 touch 命令在 ZeTianShop 目录创建 zetian.txt，并通过图形化页面编辑并保存如下内容：

```txt
zetian is a employee of kkfc
kkfc full name is KunKunChickenFarm
```

过滤 zetian 关键字

```shell
grep "zetian" zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# grep "zetian" zetian.txt
zetian is a employee of kkfc
```

过滤 kkcf 关键字

```shell
grep "kkfc" zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# grep "kkfc" zetian.txt
zetian is a employee of kkfc
kkfc full name is KunKunChickenFarm
```

过滤 full 关键字，并显示行号

```shell
grep -n "full" zetian.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# grep -n "full" zetian.txt
2:kkfc full name is KunKunChickenFarm
```

## 二、wc 命令







不加选项：行数，单词数，字节数，文件名

---

管道符



使用：

cat 管道符 grep

cat 管道符 wc

ls 管道符 grep

ls 管道符 wc

cat 管道符 grep 管道入 grep

---

练习