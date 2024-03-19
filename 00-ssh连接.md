# SSH 连接

确认本地是否有安装 ssh

```shell
ssh -v # 大写 V
```

在服务端，确认 sshd 服务的状态。

```shell
systemctl status sshd
```

> d 是 daemon 的意思，表示进程。

## 一、ssh 密码连接

连接客户端

语法：`ssh 用户名@主机`

```SHE
ssh root@66.66.66.66
```

然后会提示输入密码。

在本地打开 `~/.ssh/known_hosts`  文件（Windows 在该路径 `"C:\Users\用户名\.ssh\known_hosts"`）

这里面，记录了本地尝试过的远程连接主机

## 二、ssh 密钥连接

### 1.密钥对创建

在本地，创建 ssh 私钥和公钥，创建的私钥，放在客户端；创建的公钥，放在服务端。

```shell
ssh-keygen -t ed25519 -C "注释，通常是邮箱"
```

创建的密钥名称默认是 `id_ed25519` 和 `id_ed25519.pub`，同名的新的密钥对，会覆盖旧密钥对。

连续输入两次 passphrase，进行设置（推荐设置，也可直接回车忽略设置）。

至此，密钥对生成完成了。

通过输入以下命令，您可以更改现有私钥的密码而无需重新生成密钥对：

```shell
ssh-keygen -p -f ~/.ssh/id_ed25519
```

```she;;
$ ssh-keygen -p -f ~/.ssh/id_ed25519
> Enter old passphrase: [Type old passphrase]
> Key has comment 'your_email@example.com'
> Enter new passphrase (empty for no passphrase): [Type new passphrase]
> Enter same passphrase again: [Repeat the new passphrase]
> Your identification has been saved with the new passphrase.
```

### 2.公钥放到服务器上

在服务端，打开 `~/.ssh/authorized_keys` 文件，里面存放了要连接的客户端的公钥。

在本地，执行命令，将公钥放入服务端的 authorized_keys 文件中。

语法：`ssh-copy-id -i 本地公钥路径 用户名@主机`

```shell
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@66.66.66.66
```

> -i，i 是 identityfile，表示验证身份文件。

### 3.在本地连接服务器

现在，在本地，就可以使用密钥的方式，连接远程服务器了。

语法：`ssh -i 本地私钥路径 用户名@主机`

```shell
ssh -i ~/.ssh/id_ed25519 root@66.66.66.66
```

### 4.在服务器设置仅 ssh 连接

### 5.在本地配置 ssh

进入本地的 `~/.ssh/config` （Windows 在该路径 `"C:\Users\用户名\.ssh\config"`）文件。

配置 ssh 连接：

```shell
Host ZetianDeCentOS7
  HostName 66.66.66.66 # 主机
  IdentityFile "/Users/zetian/.ssh/id_ed25519"
  User root
```

配置完成后，在本地，使用 ssh 密钥远程连接服务器：

```shell
ssh ZetianDeCentOS7
```

### 6.ssh-agent 管理 passphrase

在本地，执行命令，让 ssh-agent 在后台运行：

```shell
eval "$(ssh-agent)"
```

然后把本地的私钥，添加给代理：

```shell
ssh-add ~/.ssh/id_ed25519
```

此时，会提示输入 passphrase。

完成后，即可使用 ssh-agent 完成 passphrase 管理，不用频繁输入 passphrase。

ssh-agent 只会把 passphrase 写入内存，但依旧存在风险。因此建议及时关闭代理，执行命令：

```shell
ssh-agent -k
```
