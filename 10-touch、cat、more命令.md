# touch、cat、more命令

## 一、touch 命令创建文件

语法：`touch Linux路径`

touch 命令无选项，参数必填，表示要创建的文件路径。

在当前工作目录的 zetian 目录内，创建 test.txt 文件

````shell
touch /zetian/test.txt
````

## 二、cat 命令查看文件内容

准备好文件内容后，通过 cat 命令查看内容。

语法：`cat Linux路径`

cat 没有选项，只有必填参数，参数表示：被查看的文件路径。

```shell
cat ~/ZeTianShop/test.txt
```

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ~]# cat ~/ZeTianShop/test.txt
hahah, hello, word, abaaba
```

## 三、more 命令查看文件内容

more 命令同样可以查看文件内容，与 cat 不同的是：more 支持翻页，如果文件内容过多，可以一页一页的展示。

- 使用空格翻页。
- 使用 q 键退出查看。

语法：`more Linux路径`

同样没有选项，只有必填参数，参数表示：被查看的文件路径。

查看 /etc/services 文件

```shell
more /etc/services
```
