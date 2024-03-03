# Linux 命令基础

## 一、命令、命令行

学习 Linux，本质上是学习在命令行下，熟练使用 Linux 的各类命令。

命令行：即 Linux 终端（Terminal），是一种命令提示符界面，使用各种字符化的命令，对系统发出操作指令。

命令：即 Linux 程序，一个命令，就是一个 Linux 程序。命令没有图形化界面，只能在命令行中提供字符化反馈。

FinalShell 就是一个命令行程序。

## 二、Linux 命令的基础格式

`command [-options] [parameter]`

- command：命令本身。
- options：[可选，非必填] 命令的一些选项，可以通过选项控制命令的行为细节。
- parameter：[可选，非必填] 命令的参数，多数用于命令的指向目标。

示例：

`ls -l /home/zetian`，

- `ls` 是命令本身，`-l` 是选项；`/home/zetian` 是参数；
- 意思是：以列表的形式，显示 /home/zetian 下的内容。

`cp -r test1 test2`，

- `cp` 是命令本身，`-r` 是选项，`test1 test2` 是参数。
- 意思是：复制文件夹 test1 成为 test2