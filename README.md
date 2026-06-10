<div align="center">

# CrabCode · 蟹码

**终端原生的 AI 编程助手**<br>
**A terminal-native AI coding assistant**

[![Latest Release](https://img.shields.io/github/v/release/acosmi/crabcode?display_name=tag&label=latest)](https://github.com/acosmi/crabcode/releases/latest)
[![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20Windows-blue)](#当前发布)
[![Status](https://img.shields.io/badge/status-active-success)](https://github.com/acosmi/crabcode/releases)
[![Issues](https://img.shields.io/github/issues/acosmi/crabcode?label=issues)](https://github.com/acosmi/crabcode/issues)

[简体中文](#简体中文) · [English](#english)

</div>

---

## 两种使用形态 · Two Editions

CrabCode 提供两种使用形态，共享同一套账号、词元和能力。<br>
CrabCode ships in two editions that share the same account, tokens, and capabilities.

| 形态 · Edition | 说明 · Description | 获取 · Get it |
|---|---|---|
| 🖥️ **桌面 GUI 版**<br>Desktop GUI | 图形界面桌面应用，开箱即用，适合偏好可视化操作的用户。<br>A graphical desktop app, ready to use — ideal if you prefer a visual workflow. | **官网下载 · Official download**<br><https://acosmi.com/zh/downloads> |
| ⌨️ **命令行 TUI 版**<br>Terminal TUI | 终端原生全屏体验，贴近工程目录，适合 CLI、远程和自动化场景。<br>A terminal-native fullscreen experience, close to your project directory — great for CLI, remote, and automation. | **GitHub 发布页 · GitHub Releases**<br>见下方安装说明 · see install steps below |

> 本仓库（GitHub）发布的是命令行 TUI 版的安装包；桌面 GUI 版请前往官网下载页获取。<br>
> This repository (GitHub) hosts the terminal TUI packages; for the desktop GUI, use the official downloads page above.

---

## 新用户福利 · New User Offer

> 新用户注册即享 **免费一个月 Basic 基础版会员**，赠送 **6000 万 Credits**，畅用 DeepSeek、Qwen3.7、MiniMax-M3、GLM-5.1 等国内主流模型，覆盖编码、对话、工具调用与深度思考全场景。
>
> New users enjoy a **free one-month Basic membership** with **60 million Credits**, powered by leading Chinese models — DeepSeek, Qwen3.7, MiniMax-M3, GLM-5.1 and more — across coding, chat, tool use, and deep thinking.

- 注册 / Sign up: <https://acosmi.com/zh>
- 注册后在 CrabCode 中执行 `/login` 即可激活会员与额度。
- After signup, run `/login` inside CrabCode to activate your membership and Credits.
- 老用户邀请新用户可额外获得奖励。
- Existing users can earn bonus rewards by referring new users.

---

## 简体中文

### 简介

**CrabCode（蟹码）** 是一款运行在终端里的 AI 编程助手，把模型调用、代码检索、文件编辑、Shell 执行、MCP 工具和 GitHub 工作流收进同一套命令行体验。你无需离开当前工程目录，就能完成代码理解、排错、重构、测试生成与日常自动化。

这个公开仓库用于发布命令行 TUI 版的稳定安装包和面向用户的说明。**最新版本为 v1.3.40**（2026-06-07 UTC，Windows 优先发布）：Windows 平台已更新至 **v1.3.40**，macOS / Linux 当前稳定版仍为 **v1.3.38**，对应平台的 v1.3.40 安装包即将跟进。如需图形界面桌面版（GUI），请前往官方下载页：<https://acosmi.com/zh/downloads>。

### 当前发布

| 平台 | 架构 | 版本 | 发布包 |
|---|---:|:---:|---|
| macOS Apple Silicon | arm64 | 1.3.38 | `crabcode-1.3.38-darwin-arm64.tar.gz` |
| macOS Intel | x64 | 1.3.38 | `crabcode-1.3.38-darwin-x64.tar.gz` |
| Linux | arm64 | 1.3.38 | `crabcode-1.3.38-linux-arm64.tar.gz` |
| Linux | x64 | 1.3.38 | `crabcode-1.3.38-linux-x64.tar.gz` |
| Windows | x64 | **1.3.40** | `crabcode-1.3.40-win-x64.zip` |

> Windows 当前为 v1.3.40，macOS / Linux 当前为 v1.3.38；请按下方对应平台的安装命令使用匹配的版本号。

所有发布包都在 [Releases](https://github.com/acosmi/crabcode/releases) 页面提供，并附带 SHA-256 校验文件。

### 核心能力

- **终端原生 TUI**：全屏交互、流式输出、历史会话、主题和中英文界面。
- **模型动态路由**：可用模型、能力和价格由 Acosmi SDK 动态下发；在客户端内使用 `/model` 查看和切换。
- **工程级工具**：读取、写入、精确编辑、全文检索、Glob 匹配、沙盒化 Shell、Notebook 读写。
- **MCP 生态**：支持配置和调用 Model Context Protocol 服务器，包括浏览器自动化、外部数据源和自定义工具。
- **工作流增强**：Hooks、Skills、Plan Mode、权限管理、Git / GitHub 协作、跨会话记忆。
- **定时任务**：`crabcode cron` 使用独立 Rust 调度守护进程，支持 macOS、Linux 和 Windows。

### 架构状态

CrabCode 当前是 **Rust 底层核心 + TypeScript 业务层**：

| 组件 | 作用 |
|---|---|
| `crabcode` | Rust CLI 启动器，解析高频参数并启动交互式客户端 |
| `dist/index.js` | TypeScript 业务层，负责 TUI、agent loop、模型 SDK、MCP 和工具编排 |
| `crabcode-cron` | Rust 定时任务守护进程；Unix 使用 socket，Windows 使用 Named Pipe |
| `dist/vendor/ripgrep` | 随包内置的 ripgrep，用于高速代码搜索 |

历史 Hub / Go 守护进程路径已下线；模型与账户能力通过 `@acosmi/sdk-ts` 直连 Acosmi 网关。

### 安装

#### macOS

下面的命令会自动识别芯片，Apple Silicon（含 M1–M4 等 M 系列）与 Intel 通用，无需手动改：

```bash
VERSION=1.3.38
# 自动识别芯片：Apple Silicon = arm64，Intel = x86_64
case "$(uname -m)" in
  arm64)  PLATFORM=darwin-arm64 ;;
  x86_64) PLATFORM=darwin-x64 ;;
  *) echo "不支持的架构: $(uname -m)"; exit 1 ;;
esac

curl -fsSL -o /tmp/crabcode.tar.gz \
  "https://github.com/acosmi/crabcode/releases/download/v${VERSION}/crabcode-${VERSION}-${PLATFORM}.tar.gz"

rm -rf "$HOME/.local/share/crabcode"
mkdir -p "$HOME/.local/share/crabcode"
tar -xzf /tmp/crabcode.tar.gz --strip-components=1 -C "$HOME/.local/share/crabcode"

xattr -dr com.apple.quarantine "$HOME/.local/share/crabcode" 2>/dev/null || true
# 把安装目录加入 PATH（不要用跨目录 symlink：launcher 需从安装目录解析 dist/bun/orchestrator）
SHELL_RC="$HOME/.zshrc"; [ -n "$BASH_VERSION" ] && SHELL_RC="$HOME/.bashrc"
grep -q '/.local/share/crabcode' "$SHELL_RC" 2>/dev/null || \
  echo 'export PATH="$HOME/.local/share/crabcode:$PATH"' >> "$SHELL_RC"
export PATH="$HOME/.local/share/crabcode:$PATH"

crabcode --version
crabcode
```

上面的命令已自动把 `~/.local/share/crabcode` 写入 `~/.zshrc`（或 `~/.bashrc`）。若重开终端后仍提示找不到 `crabcode`，手动加入这一行：

```bash
export PATH="$HOME/.local/share/crabcode:$PATH"
```

#### Linux

下面的命令会自动识别架构（x64 与 arm64 通用），无需手动改：

```bash
VERSION=1.3.38
# 自动识别架构：x64 = x86_64，arm64 = aarch64
case "$(uname -m)" in
  x86_64|amd64)  PLATFORM=linux-x64 ;;
  aarch64|arm64) PLATFORM=linux-arm64 ;;
  *) echo "不支持的架构: $(uname -m)"; exit 1 ;;
esac

curl -fsSL -o /tmp/crabcode.tar.gz \
  "https://github.com/acosmi/crabcode/releases/download/v${VERSION}/crabcode-${VERSION}-${PLATFORM}.tar.gz"

rm -rf "$HOME/.local/share/crabcode"
mkdir -p "$HOME/.local/share/crabcode"
tar -xzf /tmp/crabcode.tar.gz --strip-components=1 -C "$HOME/.local/share/crabcode"
if command -v xattr >/dev/null 2>&1; then
  xattr -dr com.apple.quarantine "$HOME/.local/share/crabcode" 2>/dev/null || true
fi
# 把安装目录加入 PATH（不要用跨目录 symlink：launcher 需从安装目录解析 dist/bun/orchestrator）
SHELL_RC="$HOME/.zshrc"; [ -n "$BASH_VERSION" ] && SHELL_RC="$HOME/.bashrc"
grep -q '/.local/share/crabcode' "$SHELL_RC" 2>/dev/null || \
  echo 'export PATH="$HOME/.local/share/crabcode:$PATH"' >> "$SHELL_RC"
export PATH="$HOME/.local/share/crabcode:$PATH"

crabcode --version
crabcode
```

#### Windows

在 **PowerShell** 中执行，不要粘贴到 CMD/命令提示符。正确提示符通常以 `PS ` 开头，例如 `PS C:\Users\you>`；如果看到 `C:\Windows\System32>` 并报 `'$Version' 不是内部或外部命令`，说明当前在 CMD 中，需要先打开 PowerShell，或在 CMD 中输入 `powershell` 后再执行。

`win-x64` 适用于 Intel 和 AMD 的 64 位 Windows 设备。

运行交互式 TUI 时请使用 **Windows Terminal** 或新版 PowerShell 窗口，并从普通用户目录启动，例如 `C:\Users\you\Desktop>`。老式 CMD/命令提示符，尤其是管理员窗口里的 `C:\Windows\System32>`，可能出现程序已启动但界面不刷新、黑屏或只显示光标的现象；这不是安装包损坏。若必须使用旧 CMD，先执行 `chcp 65001`，并在命令提示符属性中关闭 legacy console / 旧版控制台模式。

中国大陆网络推荐使用镜像安装命令。可以直接粘贴到 CMD 或 PowerShell 中执行（镜像脚本当前提供 v1.3.38；如需 Windows 最新版 **v1.3.40**，请使用下方的 GitHub 原始下载命令）：

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol=[Net.SecurityProtocolType]::Tls12; iex ((New-Object Net.WebClient).DownloadString('https://updates.acosmi.com/crabcode/install-win-1.3.38.ps1?v=4'))"
```

如果镜像不可用，再使用下面的 GitHub 原始下载命令：

```powershell
$Version = "1.3.40"
$Package = "crabcode-$Version-win-x64"
$Zip = "$env:TEMP\$Package.zip"
$InstallRoot = "$env:LOCALAPPDATA\crabcode"
$LegacyRoot = "$env:LOCALAPPDATA\CrabCode"
$Bin = Join-Path $InstallRoot $Package

Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v$Version/$Package.zip" `
  -OutFile $Zip

Remove-Item $Bin -Recurse -Force -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Force -Path $InstallRoot | Out-Null
Expand-Archive -Path $Zip -DestinationPath $InstallRoot -Force

function Remove-CrabCodePathEntries {
  param([string]$PathValue)
  @($PathValue -split ";" | Where-Object {
    $Entry = $_.Trim()
    $Entry -and
      ($Entry -ine $InstallRoot) -and
      ($Entry -ine $LegacyRoot) -and
      ($Entry -inotlike "$InstallRoot\crabcode-*") -and
      ($Entry -inotlike "$LegacyRoot\crabcode-*")
  })
}

$UserPath = Remove-CrabCodePathEntries ([Environment]::GetEnvironmentVariable("Path", "User"))
[Environment]::SetEnvironmentVariable("Path", (($UserPath + $Bin) -join ";"), "User")

$ProcessPath = Remove-CrabCodePathEntries $env:Path
$env:Path = (($ProcessPath + $Bin) -join ";")

crabcode --version
crabcode
```

安装完成后，当前 PowerShell 和新打开的 PowerShell 都可以直接运行 `crabcode`。

#### 覆盖更新已安装版本

覆盖更新只替换程序文件，不会删除本地配置、登录状态、历史记录和记忆数据。不要删除 `~/.crabcode/`。

macOS / Linux 使用同一安装目录，重新执行下面的命令即可覆盖旧版本。命令会自动识别系统与芯片/架构，mac（Apple Silicon / Intel）与 Linux（x64 / arm64）通用：

```bash
VERSION=1.3.38
# 自动识别系统与芯片/架构（macOS 与 Linux 通用）
case "$(uname -s)-$(uname -m)" in
  Darwin-arm64)               PLATFORM=darwin-arm64 ;;
  Darwin-x86_64)              PLATFORM=darwin-x64 ;;
  Linux-x86_64|Linux-amd64)   PLATFORM=linux-x64 ;;
  Linux-aarch64|Linux-arm64)  PLATFORM=linux-arm64 ;;
  *) echo "不支持的平台: $(uname -s)-$(uname -m)"; exit 1 ;;
esac

curl -fsSL -o /tmp/crabcode.tar.gz \
  "https://github.com/acosmi/crabcode/releases/download/v${VERSION}/crabcode-${VERSION}-${PLATFORM}.tar.gz"

rm -rf "$HOME/.local/share/crabcode"
mkdir -p "$HOME/.local/share/crabcode"
tar -xzf /tmp/crabcode.tar.gz --strip-components=1 -C "$HOME/.local/share/crabcode"
if command -v xattr >/dev/null 2>&1; then
  xattr -dr com.apple.quarantine "$HOME/.local/share/crabcode" 2>/dev/null || true
fi
# 把安装目录加入 PATH（不要用跨目录 symlink：launcher 需从安装目录解析 dist/bun/orchestrator）
SHELL_RC="$HOME/.zshrc"; [ -n "$BASH_VERSION" ] && SHELL_RC="$HOME/.bashrc"
grep -q '/.local/share/crabcode' "$SHELL_RC" 2>/dev/null || \
  echo 'export PATH="$HOME/.local/share/crabcode:$PATH"' >> "$SHELL_RC"
export PATH="$HOME/.local/share/crabcode:$PATH"

crabcode --version
```

Windows 安装目录带版本号，更新时需要把用户 `PATH` 中旧的 `crabcode-*` 目录替换为新版本目录。以下命令仍然必须在 **PowerShell** 中执行，不要粘贴到 CMD/命令提示符：

```powershell
$Version = "1.3.40"
$Package = "crabcode-$Version-win-x64"
$Zip = "$env:TEMP\$Package.zip"
$InstallRoot = "$env:LOCALAPPDATA\crabcode"
$LegacyRoot = "$env:LOCALAPPDATA\CrabCode"
$Bin = Join-Path $InstallRoot $Package

Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v$Version/$Package.zip" `
  -OutFile $Zip

Remove-Item $Bin -Recurse -Force -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Force -Path $InstallRoot | Out-Null
Expand-Archive -Path $Zip -DestinationPath $InstallRoot -Force

function Remove-CrabCodePathEntries {
  param([string]$PathValue)
  @($PathValue -split ";" | Where-Object {
    $Entry = $_.Trim()
    $Entry -and
      ($Entry -ine $InstallRoot) -and
      ($Entry -ine $LegacyRoot) -and
      ($Entry -inotlike "$InstallRoot\crabcode-*") -and
      ($Entry -inotlike "$LegacyRoot\crabcode-*")
  })
}

$UserPath = Remove-CrabCodePathEntries ([Environment]::GetEnvironmentVariable("Path", "User"))
[Environment]::SetEnvironmentVariable("Path", (($UserPath + $Bin) -join ";"), "User")

$ProcessPath = Remove-CrabCodePathEntries $env:Path
$env:Path = (($ProcessPath + $Bin) -join ";")

crabcode --version
```

更新前请退出正在运行的 CrabCode；更新完成后，当前 PowerShell 和新打开的 PowerShell 都会使用新版本。

### 校验文件完整性

在已下载发布包的目录中执行：

```bash
curl -fsSL -O https://github.com/acosmi/crabcode/releases/download/v1.3.38/checksums-sha256.txt
shasum -a 256 -c checksums-sha256.txt
```

Linux 也可以使用：

```bash
sha256sum -c checksums-sha256.txt
```

Windows 可下载 Windows 专用校验文件后对比：

```powershell
Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v1.3.40/checksums-sha256.txt" `
  -OutFile checksums-sha256.txt

$Expected = (Select-String -Path checksums-sha256.txt -Pattern "crabcode-1.3.40-win-x64.zip").Line.Split()[0].ToLower()
$Actual = (Get-FileHash crabcode-1.3.40-win-x64.zip -Algorithm SHA256).Hash.ToLower()
if ($Expected -ne $Actual) {
  throw "SHA256 mismatch: expected $Expected, got $Actual"
}
"SHA256 OK: $Actual"
```

### 快速上手

```bash
crabcode               # 进入交互式 TUI
crabcode -p "解释当前目录的代码结构"
crabcode --help
crabcode --version
```

第一次使用请在 TUI 中执行 `/login` 完成账号认证。

常用命令：

| 命令 | 用途 |
|---|---|
| `/login` | 登录或切换账号 |
| `/model` | 查看和切换可用模型 |
| `/clear` | 清空当前会话上下文 |
| `/history` | 查看历史会话 |
| `/permissions` | 查看或修改工具权限 |
| `/help` | 打开帮助 |

常用快捷键：

| 操作 | 按键 |
|---|---|
| 切换思考档位 | `Tab` |
| 中断当前任务 | `Esc` |
| 翻阅历史 | `↑` / `↓` |
| 滚动屏幕 | `PgUp` / `PgDn` 或鼠标滚轮 |
| 退出 | 连续按两次 `Ctrl+C` |

### 数据与隐私

- 用户配置、认证状态、历史和本地记忆默认保存在 `~/.crabcode/`。
- 工具执行默认受权限控制；文件和 Shell 操作需要按目录授权。
- 模型请求经由 Acosmi 网关转发到上游模型服务；具体可用模型和额度以账号状态为准。

### 反馈与支持

- Bug / 建议: <https://github.com/acosmi/crabcode/issues>
- 最新发布: <https://github.com/acosmi/crabcode/releases/latest>
- 官方网站: <https://acosmi.com/zh>
- 账号和词元问题：登录账户后台，或在 CrabCode 中执行 `/help`。

---

## English

### Overview

**CrabCode** is a terminal-native AI coding assistant that brings model access, code search, file editing, shell execution, MCP tools, and GitHub workflows into one command-line experience. Without leaving the project directory you are already in, you can understand code, debug, refactor, generate tests, and automate everyday engineering tasks.

This public repository hosts the terminal TUI release packages and user-facing documentation. **The latest release is v1.3.40** (2026-06-07 UTC, Windows-first): the Windows package is updated to **v1.3.40**, while macOS / Linux stay on the **v1.3.38** stable build for now — v1.3.40 packages for those platforms will follow. For the graphical desktop app (GUI), use the official downloads page: <https://acosmi.com/zh/downloads>.

### Current Release

| Platform | Architecture | Version | Asset |
|---|---:|:---:|---|
| macOS Apple Silicon | arm64 | 1.3.38 | `crabcode-1.3.38-darwin-arm64.tar.gz` |
| macOS Intel | x64 | 1.3.38 | `crabcode-1.3.38-darwin-x64.tar.gz` |
| Linux | arm64 | 1.3.38 | `crabcode-1.3.38-linux-arm64.tar.gz` |
| Linux | x64 | 1.3.38 | `crabcode-1.3.38-linux-x64.tar.gz` |
| Windows | x64 | **1.3.40** | `crabcode-1.3.40-win-x64.zip` |

> Windows is on v1.3.40 and macOS / Linux are on v1.3.38; use the version number that matches your platform's install commands below.

All packages are available on the [Releases](https://github.com/acosmi/crabcode/releases) page with SHA-256 checksum files.

### Core Features

- **Terminal-native TUI**: fullscreen interaction, streaming output, session history, themes, and English / Chinese UI.
- **Dynamic model routing**: available models, capabilities, and pricing are provided dynamically by the Acosmi SDK; use `/model` in the client to inspect and switch.
- **Engineering tools**: read, write, exact edit, full-text search, Glob matching, sandboxed Shell, and Notebook read/write.
- **MCP ecosystem**: configure and call Model Context Protocol servers for browser automation, external data, and custom tools.
- **Workflow support**: Hooks, Skills, Plan Mode, permissions, Git / GitHub collaboration, and cross-session memory.
- **Scheduled tasks**: `crabcode cron` uses an independent Rust scheduler daemon on macOS, Linux, and Windows.

### Architecture Status

CrabCode currently uses a **Rust core + TypeScript product layer**:

| Component | Role |
|---|---|
| `crabcode` | Rust CLI launcher that parses high-frequency flags and starts the interactive client |
| `dist/index.js` | TypeScript layer for TUI, agent loop, model SDK, MCP, and tool orchestration |
| `crabcode-cron` | Rust scheduled-task daemon; Unix socket on macOS/Linux, Named Pipe on Windows |
| `dist/vendor/ripgrep` | Bundled ripgrep binary for fast code search |

The historical Hub / Go daemon path has been retired; model and account capabilities go through `@acosmi/sdk-ts` and the Acosmi gateway.

### Installation

#### macOS

The command below auto-detects your chip and works on both Apple Silicon (including the M1–M4 series) and Intel — no manual edit needed:

```bash
VERSION=1.3.38
# Auto-detect the chip: Apple Silicon = arm64, Intel = x86_64
case "$(uname -m)" in
  arm64)  PLATFORM=darwin-arm64 ;;
  x86_64) PLATFORM=darwin-x64 ;;
  *) echo "Unsupported architecture: $(uname -m)"; exit 1 ;;
esac

curl -fsSL -o /tmp/crabcode.tar.gz \
  "https://github.com/acosmi/crabcode/releases/download/v${VERSION}/crabcode-${VERSION}-${PLATFORM}.tar.gz"

rm -rf "$HOME/.local/share/crabcode"
mkdir -p "$HOME/.local/share/crabcode"
tar -xzf /tmp/crabcode.tar.gz --strip-components=1 -C "$HOME/.local/share/crabcode"

xattr -dr com.apple.quarantine "$HOME/.local/share/crabcode" 2>/dev/null || true
# 把安装目录加入 PATH（不要用跨目录 symlink：launcher 需从安装目录解析 dist/bun/orchestrator）
SHELL_RC="$HOME/.zshrc"; [ -n "$BASH_VERSION" ] && SHELL_RC="$HOME/.bashrc"
grep -q '/.local/share/crabcode' "$SHELL_RC" 2>/dev/null || \
  echo 'export PATH="$HOME/.local/share/crabcode:$PATH"' >> "$SHELL_RC"
export PATH="$HOME/.local/share/crabcode:$PATH"

crabcode --version
crabcode
```

The command above already appends `~/.local/share/crabcode` to `~/.zshrc` (or `~/.bashrc`). If `crabcode` is still not found after reopening your terminal, add this line manually:

```bash
export PATH="$HOME/.local/share/crabcode:$PATH"
```

#### Linux

The command below auto-detects your architecture and works on both x64 and arm64 — no manual edit needed:

```bash
VERSION=1.3.38
# Auto-detect the architecture: x64 = x86_64, arm64 = aarch64
case "$(uname -m)" in
  x86_64|amd64)  PLATFORM=linux-x64 ;;
  aarch64|arm64) PLATFORM=linux-arm64 ;;
  *) echo "Unsupported architecture: $(uname -m)"; exit 1 ;;
esac

curl -fsSL -o /tmp/crabcode.tar.gz \
  "https://github.com/acosmi/crabcode/releases/download/v${VERSION}/crabcode-${VERSION}-${PLATFORM}.tar.gz"

rm -rf "$HOME/.local/share/crabcode"
mkdir -p "$HOME/.local/share/crabcode"
tar -xzf /tmp/crabcode.tar.gz --strip-components=1 -C "$HOME/.local/share/crabcode"
if command -v xattr >/dev/null 2>&1; then
  xattr -dr com.apple.quarantine "$HOME/.local/share/crabcode" 2>/dev/null || true
fi
# 把安装目录加入 PATH（不要用跨目录 symlink：launcher 需从安装目录解析 dist/bun/orchestrator）
SHELL_RC="$HOME/.zshrc"; [ -n "$BASH_VERSION" ] && SHELL_RC="$HOME/.bashrc"
grep -q '/.local/share/crabcode' "$SHELL_RC" 2>/dev/null || \
  echo 'export PATH="$HOME/.local/share/crabcode:$PATH"' >> "$SHELL_RC"
export PATH="$HOME/.local/share/crabcode:$PATH"

crabcode --version
crabcode
```

#### Windows

Run this in **PowerShell**, not in Command Prompt/CMD. A correct prompt usually starts with `PS `, for example `PS C:\Users\you>`. If you see `C:\Windows\System32>` and get `'$Version' is not recognized as an internal or external command`, you are in CMD; open PowerShell first, or type `powershell` in CMD before running the commands.

`win-x64` works on both Intel and AMD 64-bit Windows devices.

Run the interactive TUI in **Windows Terminal** or a modern PowerShell window, and start it from a normal user directory such as `C:\Users\you\Desktop>`. Legacy Command Prompt/CMD, especially an elevated `C:\Windows\System32>` window, may make the app look frozen, blank, or show only a cursor even though the executable has started. This is not a corrupt installation. If you must use legacy CMD, run `chcp 65001` first and disable legacy console mode in Command Prompt properties.

For networks where GitHub is slow or unstable, use the mirror installer. This one-liner can be pasted into either CMD or PowerShell (the mirror currently serves v1.3.38; for the latest Windows **v1.3.40**, use the GitHub download commands below):

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol=[Net.SecurityProtocolType]::Tls12; iex ((New-Object Net.WebClient).DownloadString('https://updates.acosmi.com/crabcode/install-win-1.3.38.ps1?v=4'))"
```

If the mirror is unavailable, use the original GitHub download commands below:

```powershell
$Version = "1.3.40"
$Package = "crabcode-$Version-win-x64"
$Zip = "$env:TEMP\$Package.zip"
$InstallRoot = "$env:LOCALAPPDATA\crabcode"
$LegacyRoot = "$env:LOCALAPPDATA\CrabCode"
$Bin = Join-Path $InstallRoot $Package

Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v$Version/$Package.zip" `
  -OutFile $Zip

Remove-Item $Bin -Recurse -Force -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Force -Path $InstallRoot | Out-Null
Expand-Archive -Path $Zip -DestinationPath $InstallRoot -Force

function Remove-CrabCodePathEntries {
  param([string]$PathValue)
  @($PathValue -split ";" | Where-Object {
    $Entry = $_.Trim()
    $Entry -and
      ($Entry -ine $InstallRoot) -and
      ($Entry -ine $LegacyRoot) -and
      ($Entry -inotlike "$InstallRoot\crabcode-*") -and
      ($Entry -inotlike "$LegacyRoot\crabcode-*")
  })
}

$UserPath = Remove-CrabCodePathEntries ([Environment]::GetEnvironmentVariable("Path", "User"))
[Environment]::SetEnvironmentVariable("Path", (($UserPath + $Bin) -join ";"), "User")

$ProcessPath = Remove-CrabCodePathEntries $env:Path
$env:Path = (($ProcessPath + $Bin) -join ";")

crabcode --version
crabcode
```

After the block completes, `crabcode` works in this PowerShell window and in newly opened PowerShell windows.

#### Update an Existing Installation

An update only replaces application files. It does not remove local config, auth state, history, or memory data. Do not delete `~/.crabcode/`.

On macOS / Linux, reinstall into the same application directory to overwrite the old version. The command auto-detects your OS and chip/architecture, working on both macOS (Apple Silicon / Intel) and Linux (x64 / arm64):

```bash
VERSION=1.3.38
# Auto-detect OS and chip/architecture (works on both macOS and Linux)
case "$(uname -s)-$(uname -m)" in
  Darwin-arm64)               PLATFORM=darwin-arm64 ;;
  Darwin-x86_64)              PLATFORM=darwin-x64 ;;
  Linux-x86_64|Linux-amd64)   PLATFORM=linux-x64 ;;
  Linux-aarch64|Linux-arm64)  PLATFORM=linux-arm64 ;;
  *) echo "Unsupported platform: $(uname -s)-$(uname -m)"; exit 1 ;;
esac

curl -fsSL -o /tmp/crabcode.tar.gz \
  "https://github.com/acosmi/crabcode/releases/download/v${VERSION}/crabcode-${VERSION}-${PLATFORM}.tar.gz"

rm -rf "$HOME/.local/share/crabcode"
mkdir -p "$HOME/.local/share/crabcode"
tar -xzf /tmp/crabcode.tar.gz --strip-components=1 -C "$HOME/.local/share/crabcode"
if command -v xattr >/dev/null 2>&1; then
  xattr -dr com.apple.quarantine "$HOME/.local/share/crabcode" 2>/dev/null || true
fi
# 把安装目录加入 PATH（不要用跨目录 symlink：launcher 需从安装目录解析 dist/bun/orchestrator）
SHELL_RC="$HOME/.zshrc"; [ -n "$BASH_VERSION" ] && SHELL_RC="$HOME/.bashrc"
grep -q '/.local/share/crabcode' "$SHELL_RC" 2>/dev/null || \
  echo 'export PATH="$HOME/.local/share/crabcode:$PATH"' >> "$SHELL_RC"
export PATH="$HOME/.local/share/crabcode:$PATH"

crabcode --version
```

On Windows, the install directory includes the version number, so update the user `PATH` to replace old `crabcode-*` directories with the new one. Run the following commands in **PowerShell**, not in Command Prompt/CMD:

```powershell
$Version = "1.3.40"
$Package = "crabcode-$Version-win-x64"
$Zip = "$env:TEMP\$Package.zip"
$InstallRoot = "$env:LOCALAPPDATA\crabcode"
$LegacyRoot = "$env:LOCALAPPDATA\CrabCode"
$Bin = Join-Path $InstallRoot $Package

Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v$Version/$Package.zip" `
  -OutFile $Zip

Remove-Item $Bin -Recurse -Force -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Force -Path $InstallRoot | Out-Null
Expand-Archive -Path $Zip -DestinationPath $InstallRoot -Force

function Remove-CrabCodePathEntries {
  param([string]$PathValue)
  @($PathValue -split ";" | Where-Object {
    $Entry = $_.Trim()
    $Entry -and
      ($Entry -ine $InstallRoot) -and
      ($Entry -ine $LegacyRoot) -and
      ($Entry -inotlike "$InstallRoot\crabcode-*") -and
      ($Entry -inotlike "$LegacyRoot\crabcode-*")
  })
}

$UserPath = Remove-CrabCodePathEntries ([Environment]::GetEnvironmentVariable("Path", "User"))
[Environment]::SetEnvironmentVariable("Path", (($UserPath + $Bin) -join ";"), "User")

$ProcessPath = Remove-CrabCodePathEntries $env:Path
$env:Path = (($ProcessPath + $Bin) -join ";")

crabcode --version
```

Exit running CrabCode sessions before updating. After the update, this PowerShell window and newly opened PowerShell windows use the new version.

### Verify File Integrity

Run this in the directory where you downloaded the release packages:

```bash
curl -fsSL -O https://github.com/acosmi/crabcode/releases/download/v1.3.38/checksums-sha256.txt
shasum -a 256 -c checksums-sha256.txt
```

On Linux you can also use:

```bash
sha256sum -c checksums-sha256.txt
```

For Windows:

```powershell
Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v1.3.40/checksums-sha256.txt" `
  -OutFile checksums-sha256.txt

$Expected = (Select-String -Path checksums-sha256.txt -Pattern "crabcode-1.3.40-win-x64.zip").Line.Split()[0].ToLower()
$Actual = (Get-FileHash crabcode-1.3.40-win-x64.zip -Algorithm SHA256).Hash.ToLower()
if ($Expected -ne $Actual) {
  throw "SHA256 mismatch: expected $Expected, got $Actual"
}
"SHA256 OK: $Actual"
```

### Quick Start

```bash
crabcode               # Interactive TUI
crabcode -p "Explain this repository"
crabcode --help
crabcode --version
```

On first use, run `/login` inside the TUI to authenticate your account.

Common slash commands:

| Command | Purpose |
|---|---|
| `/login` | Sign in or switch account |
| `/model` | Inspect and switch available models |
| `/clear` | Clear current session context |
| `/history` | View past sessions |
| `/permissions` | View or change tool permissions |
| `/help` | Open help |

Common shortcuts:

| Action | Key |
|---|---|
| Cycle thinking level | `Tab` |
| Interrupt current task | `Esc` |
| History up/down | `↑` / `↓` |
| Scroll screen | `PgUp` / `PgDn` or mouse wheel |
| Quit | `Ctrl+C` twice |

### Data & Privacy

- User configuration, auth state, history, and local memory are stored under `~/.crabcode/` by default.
- Tool execution is permission-gated by default; file and Shell access are authorized per directory.
- Model requests are routed through the Acosmi gateway to upstream model services; available models and quota depend on account status.

### Feedback & Support

- Bugs / suggestions: <https://github.com/acosmi/crabcode/issues>
- Latest release: <https://github.com/acosmi/crabcode/releases/latest>
- Official site: <https://acosmi.com/zh>
- Account and token issues: use your account dashboard, or run `/help` inside CrabCode.

---

<div align="center">

**CrabCode · Crafted by Acosmi · 2026**

</div>
