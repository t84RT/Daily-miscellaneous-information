# 安装最新的 PowerShell – 跨平台指南-小吴同学电气设计

本指南将帮助你在 **Windows**、**macOS** 和 **Linux** 上安装最新版本的 PowerShell。  
PowerShell 7 与旧版 Windows PowerShell 5.1 彼此独立，可以共存，安装新版本不会影响系统自带版本。

---

## 目录

- [在 Windows 上安装](#在-windows-上安装)
  - [使用 Winget（推荐）](#使用-winget推荐)
  - [使用 MSI 安装包（企业/服务器）](#使用-msi-安装包企业服务器)
  - [从 Microsoft Store 安装](#从-microsoft-store-安装)
- [在 macOS 上安装](#在-macos-上安装)
  - [使用 Homebrew（推荐）](#使用-homebrew推荐)
  - [手动安装 .pkg 包](#手动安装-pkg-包)
- [在 Linux 上安装](#在-linux-上安装)
  - [Ubuntu / Debian（APT）](#ubuntu--debianapt)
  - [其他 Linux 发行版](#其他-linux-发行版)
- [验证安装](#验证安装)
- [更新 PowerShell](#更新-powershell)
- [卸载 PowerShell](#卸载-powershell)
- [常见问题](#常见问题)
- [参考链接](#参考链接)

---

## 在 Windows 上安装

### 使用 Winget（推荐）

Winget 是 Windows 的官方包管理器，适用于 **Windows 11** 和 **Windows Server 2025**（以及 Windows 10 较新版本）。  

打开 **PowerShell** 或 **命令提示符**（以管理员身份运行），执行以下命令：

- **安装最新稳定版（默认 MSIX 包）**  
  ```powershell
  winget install --id Microsoft.PowerShell --source winget
  ```

- **安装 MSI 包（适合企业部署）**  
  ```powershell
  winget install --id Microsoft.PowerShell --source winget --installer-type wix
  ```

- **安装最新的预览版**  
  ```powershell
  winget install --id Microsoft.PowerShell.Preview --source winget
  ```

> **提示**：安装后，PowerShell 7 的可执行文件为 `pwsh.exe`，默认安装在 `%ProgramFiles%\PowerShell\7\`。

---

### 使用 MSI 安装包（企业/服务器）

适用于 Windows Server 及需要静默部署或离线安装的环境。

1. 访问 [GitHub 发布页面](https://aka.ms/powershell-release?tag=stable) 或 [Microsoft 官方下载页](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows)。
2. 下载适合你系统架构的 `.msi` 文件（如 `PowerShell-7.6.4-win-x64.msi`）。
3. 双击运行，按照向导完成安装。
4. （可选）如需静默安装，可使用以下命令：
   ```cmd
   msiexec /i PowerShell-7.6.4-win-x64.msi /quiet
   ```

---

### 从 Microsoft Store 安装

适合普通用户或想自动更新的人，但功能可能有极少数限制（如某些扩展支持）。

- 打开 **Microsoft Store**。
- 搜索 **“PowerShell”**。
- 点击 **“安装”** 按钮。  
  安装后可通过 Store 获得自动更新。

---

## 在 macOS 上安装

### 使用 Homebrew（推荐）

Homebrew 是 macOS 上最流行的包管理器。

1. **安装 Homebrew**（如尚未安装）：
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **安装最新稳定版 PowerShell**：
   ```bash
   brew install --cask powershell
   ```
   如需安装 **长期支持版 (LTS)**：
   ```bash
   brew install powershell/tap/powershell-lts
   ```

3. **启动 PowerShell**：
   ```bash
   pwsh
   ```

---

### 手动安装 .pkg 包

1. 前往 [GitHub 发布页面](https://aka.ms/powershell-release?tag=stable)。
2. 下载适用于你 Mac 芯片的 `.pkg` 文件：
   - Apple Silicon（M1/M2/M3）：`powershell-7.6.4-osx-arm64.pkg`
   - Intel：`powershell-7.6.4-osx-x64.pkg`
3. 双击 `.pkg` 文件，按提示完成安装。
4. 如果 macOS 提示“无法验证开发者”，请前往 **系统设置 > 隐私与安全性**，点击 **“仍然打开”**。

---

## 在 Linux 上安装

### Ubuntu / Debian（APT）

1. **更新包列表并安装依赖**：
   ```bash
   sudo apt-get update
   sudo apt-get install -y wget apt-transport-https software-properties-common
   ```

2. **下载并注册 Microsoft 存储库密钥**：
   ```bash
   wget -q https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb
   sudo dpkg -i packages-microsoft-prod.deb
   ```

3. **再次更新并安装 PowerShell**：
   ```bash
   sudo apt-get update
   sudo apt-get install -y powershell
   ```

4. **启动**：
   ```bash
   pwsh
   ```

> **注意**：对于 Ubuntu 22.04 及更高版本，上述命令会自动适配。如果 `lsb_release -rs` 返回非标准版本号，请手动替换为对应版本（如 `22.04`）。

---

### 其他 Linux 发行版

- **RHEL / CentOS / Fedora**：使用 `yum` 或 `dnf`，添加 Microsoft 仓库后执行 `sudo yum install powershell`。
- **openSUSE**：使用 `zypper`，添加仓库后执行 `sudo zypper install powershell`。
- **Alpine Linux**：需从源码编译或使用社区包。

> 详细步骤请参考 [Microsoft 官方 Linux 安装文档](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-linux)。

---

## 验证安装

安装完成后，打开终端（或 PowerShell 窗口）执行：

```powershell
pwsh --version
```

或进入 PowerShell 后执行：

```powershell
$PSVersionTable
```

你将看到版本号（例如 `7.6.4`）和详细的环境信息。

---

## 更新 PowerShell

- **Windows（Winget）**：
  ```powershell
  winget upgrade --id Microsoft.PowerShell --source winget
  ```

- **Windows（MSI）**：下载新版 MSI 重新安装（会覆盖旧版）。

- **macOS（Homebrew）**：
  ```bash
  brew update
  brew upgrade powershell
  ```

- **Linux（APT）**：
  ```bash
  sudo apt update
  sudo apt upgrade powershell
  ```

---

## 卸载 PowerShell

- **Windows（Winget）**：
  ```powershell
  winget uninstall --id Microsoft.PowerShell
  ```

- **Windows（控制面板）**：在“添加/删除程序”中找到“PowerShell 7”并卸载。

- **macOS（Homebrew）**：
  ```bash
  brew uninstall --cask powershell
  ```

- **Linux（APT）**：
  ```bash
  sudo apt remove powershell
  ```

---

## 常见问题

### Q: 安装后无法运行 `pwsh`？
- **Windows**：请确保 `pwsh.exe` 所在目录（如 `C:\Program Files\PowerShell\7\`）已添加到系统 `PATH` 环境变量。通常安装程序会自动添加。
- **macOS/Linux**：尝试重新登录终端或执行 `source ~/.bashrc`（或 `~/.zshrc`）。

### Q: 安装新旧版本如何共存？
- PowerShell 7 与 Windows PowerShell 5.1 完全独立，可同时存在。启动方式：
  - 旧版：`powershell.exe`
  - 新版：`pwsh.exe`

### Q: 如何切换默认版本？
- 在 Windows 中，你可以修改 `pwsh` 别名或调整 `PATH` 顺序，但更推荐直接使用 `pwsh` 命令调用新版。

### Q: 为什么安装的是预览版？
- 如果你使用了 `Microsoft.PowerShell.Preview` 的 Winget ID，会安装预览版。安装稳定版请使用 `Microsoft.PowerShell`。

---

## 参考链接

- [PowerShell GitHub 发布页面](https://github.com/PowerShell/PowerShell/releases)
- [Microsoft 官方安装指南（Windows）](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-windows)
- [Microsoft 官方安装指南（macOS）](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-macos)
- [Microsoft 官方安装指南（Linux）](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-linux)
- [PowerShell 文档首页](https://learn.microsoft.com/zh-cn/powershell/)

---

> **最后更新**：2026 年 9 月  
> 欢迎提交 Issue 或 PR 改进本指南。
---

###小吴同学电气设计
**Happy Scripting! 🚀**
