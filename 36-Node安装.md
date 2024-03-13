# Node 安装


在 Windows Subsystem for Linux (WSL) 的 Ubuntu 环境中安装 `n` 工具和在标准 Ubuntu 环境下的步骤基本相同。以下是具体步骤：

① 打开 WSL 及其 Ubuntu 终端。

② 首先安装 Node.js 和 npm。你可以通过以下命令安装：

```bash
sudo apt update
sudo apt install npm
```

③ 使用 npm 安装 `n`：

```bash
sudo npm install -g n
```

这时，`n` 工具已经全局安装并可以立即使用。你可以通过以下命令切换 Node.js 版本：

- 安装最新版本的 Node.js：

  ```bash
  sudo n lts
  ```

- 安装最新的稳定版本 Node.js：

  ```bash
  sudo n stable
  ```

- 安装特定版本的 Node.js，例如 v14.17.3：

  ```bash
  sudo n 14.17.3
  ```

请注意，在 WSL 中，点开一个新的终端会话（重新打开一个新的 Ubuntu 终端）后，你会在这个新会话中看到新选择的 Node.js 版本。此外，如同在一般的 Ubuntu 环境中，切换 Node.js 版本需要管理员权限，所以这些命令需要使用 `sudo` 来执行。

在安装完成后，使用 apt 卸载之前安装的 npm

```shell
apt remove npm
```

