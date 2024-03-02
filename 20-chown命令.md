# chown  命令

chown 命令，可以修改文件、文件夹的所属用户和用户组。

此命令只由 root 用户执行。

语法：`chown [-R] [用户]:[用户组] 文件或文件夹`

- `-R` 选项，对文件夹内全部内容应用相同规则。
- `用户`，选项，修改所属用户.
- `用户组`，选项，修改所属用户组。
- `:`，用于分隔用户，和用户组

示例：

`chown root abc.txt` 命令，用于将 abc.txt 所属用户修改为 root。

`chown :root abc.txt` 命令，将 abc.txt 所属用户组修改为 root

`chown root:kkcf abc.txt` 命令，用于将 abc.txt 所属用户，修改为 root，用户组修改为 kkcf

`chown -R root test` 命令，用于将文件夹 test 的所属用户修改为 root，并对文件夹内全部内容应用同样规则
