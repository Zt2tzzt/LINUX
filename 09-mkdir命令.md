# mkdir 命令

mkdir 命令用于创建新的目录（文件夹）

 mkdir来自英文：Make Directory

语法：`mkdir [-p] [Linux路径]`

- 参数必填，表示 Linux 路径，即要创建的文件夹的路径，相对路径或绝对路径均可。
- `-p` 选项可选，表示自动创建不存在的父目录，适用于创建连续多层级的目录。

使用 mkdir 命令的 -p 选项，创建不存在的多层级目录

```shell
[root@iZwz9clzmhmmlb65bbcvuuZ ZeTianShop]# mkdir -p test3/good/888
```

> 注意：创建文件夹需要修改权限，普通用户，请确保操作均在 HOME 目录内，不要在 HOME 外操作，会涉及到权限问题。

> 补充：FinalShell 快捷键：ctrl + l 清空命令行