



## 命令

在cmd或者powershell 使用`wsl -u root`初始wsl并使用管理员权限

在Ubuntu中使用`sudo su`进入管理员模式

一次`exit`退出管理员模式

------

### 🔧 1. `echo 'export PATH=/home/submerge_psc/.local/bin:$PATH' >> ~/.bashrc`

- **作用**：将 `export PATH=/home/submerge_psc/.local/bin:$PATH` 这一行添加到当前用户的 `~/.bashrc` 配置文件中。
- **解释**：
  - `export PATH=...`：设置并导出 `PATH` 环境变量，使其在当前 shell 会话及其子进程中可用。
  - `:/home/submerge_psc/.local/bin`：将 `/home/submerge_psc/.local/bin` 目录添加到 `PATH` 的开头。
  - `:$PATH`：保留原有的 `PATH` 设置，确保系统原有的可执行文件路径不受影响。
- **目的**：确保系统能够找到安装在 `/home/submerge_psc/.local/bin` 目录中的可执行文件。

------

### 🔄 2. `source ~/.bashrc`

- **作用**：使 `~/.bashrc` 配置文件中的更改立即生效，而无需重新启动终端。
- **解释**：`source` 命令会在当前 shell 会话中执行指定的文件，这样文件中的环境变量设置和配置会立即生效。
- **目的**：使之前添加到 `~/.bashrc` 中的 `PATH` 更改立即生效。