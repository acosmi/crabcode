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
| 🖥️ **桌面 GUI 版**<br>Desktop GUI | 图形界面桌面应用，开箱即用，适合偏好可视化操作的用户。<br>A graphical desktop app, ready to use — ideal if you prefer a visual workflow. | **官网下载 · Official download**<br><https://acosmi.com/zh/downloads><br>Windows 也可从本仓库 [Releases](https://github.com/acosmi/crabcode/releases/latest) 下载<br>Windows users may also download from this repo's Releases |
| ⌨️ **命令行 TUI 版**<br>Terminal TUI | 终端原生全屏体验，贴近工程目录，适合 CLI、远程和自动化场景。<br>A terminal-native fullscreen experience, close to your project directory — great for CLI, remote, and automation. | **GitHub 发布页 · GitHub Releases**<br>见下方安装说明 · see install steps below |

> 本仓库（GitHub）的 Releases 提供命令行 TUI 版（全平台）和 **Windows 图形 GUI 版**安装包；macOS / Linux 的 GUI 版请前往官网下载页获取。<br>
> This repository (GitHub) Releases host the terminal TUI packages (all platforms) and the **Windows GUI** installer; for the macOS / Linux GUI, use the official downloads page above.

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

这个公开仓库用于发布命令行 TUI 版的稳定安装包和面向用户的说明。最新版本为 **v1.3.43**，发布时间为 **2026-06-11 UTC**。如需图形界面桌面版（GUI），请前往官方下载页：<https://acosmi.com/zh/downloads>。

### 当前发布

| 平台 | 架构 | 发布包 |
|---|---:|---|
| macOS Apple Silicon | arm64 | `crabcode-1.3.43-darwin-arm64.tar.gz` |
| macOS Intel | x64 | `crabcode-1.3.43-darwin-x64.tar.gz` |
| Linux | arm64 | `crabcode-1.3.43-linux-arm64.tar.gz` |
| Linux | x64 | `crabcode-1.3.43-linux-x64.tar.gz` |
| Windows | x64 | `crabcode-1.3.43-win-x64.zip` |

所有发布包都在 [Releases](https://github.com/acosmi/crabcode/releases/latest) 页面提供，并附带 SHA-256 校验文件。

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

**macOS / Linux** — 一条命令完成安装（自动识别平台、SHA256 fail-closed 校验、自动配置 PATH）：

```bash
curl -fsSL https://updates.acosmi.com/crabcode/install.sh | sh
```

**Windows** — 在 **PowerShell** 中执行（不要粘贴进 CMD；正确提示符以 `PS ` 开头）：

```powershell
irm https://updates.acosmi.com/crabcode/install.ps1 | iex
```

说明：

- 安装源为国内镜像（`updates.acosmi.com`），镜像不可达时自动回退 GitHub Releases；校验文件与产物**同源**，SHA256 校验 fail-closed（校验不过绝不落地）。
- 海外用户也可以直接使用 GitHub 源，效果等价：

```bash
curl -fsSL https://github.com/acosmi/crabcode/releases/latest/download/install.sh | sh
```

- Windows 运行交互式 TUI 请使用 **Windows Terminal** 或新版 PowerShell 窗口，并从普通用户目录启动（例如 `C:\Users\you>`）。老式 CMD（尤其管理员窗口的 `C:\Windows\System32>`）可能出现界面不刷新或黑屏；若必须使用旧 CMD，先执行 `chcp 65001` 并关闭 legacy console 模式。
- 手动安装（高级）：从 [Releases](https://github.com/acosmi/crabcode/releases/latest) 下载对应平台压缩包，解压后把目录加入 PATH 即可。注意安装目录需**整体保留**（launcher 从同目录解析 `dist/`、`bun`、`node_modules/`、orchestrator 等，不要只拷单个二进制、不要跨目录 symlink）。

#### 更新

已安装用户一条命令更新到最新版（只替换程序文件，不动配置、登录状态、历史与记忆数据）：

```bash
crabcode update
```

也可以在 TUI 内输入 `/update`，或重跑上面的安装命令（等价覆盖安装）。

#### Windows 图形界面（GUI）版

不想用命令行的 Windows 用户，可以直接下载图形界面安装包，无需配置 PATH：

1. 打开 [最新 Release](https://github.com/acosmi/crabcode/releases/latest)，在 Assets 中下载 `crabcode-1.3.43-win-x64-setup.exe`。
2. 双击运行安装向导，按提示完成；安装后从开始菜单启动 CrabCode 桌面版。

直接下载链接：<https://github.com/acosmi/crabcode/releases/download/v1.3.43/crabcode-1.3.43-win-x64-setup.exe>

> macOS / Linux 的图形界面版请前往官网下载页：<https://acosmi.com/zh/downloads>。

### 校验文件完整性

在已下载发布包的目录中执行：

```bash
curl -fsSL -O https://github.com/acosmi/crabcode/releases/download/v1.3.43/checksums-sha256.txt
shasum -a 256 -c checksums-sha256.txt
```

Linux 也可以使用：

```bash
sha256sum -c checksums-sha256.txt
```

Windows 可下载 Windows 专用校验文件后对比：

```powershell
Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v1.3.43/checksums-sha256.txt" `
  -OutFile checksums-sha256.txt

$Expected = (Select-String -Path checksums-sha256.txt -Pattern "crabcode-1.3.43-win-x64.zip").Line.Split()[0].ToLower()
$Actual = (Get-FileHash crabcode-1.3.43-win-x64.zip -Algorithm SHA256).Hash.ToLower()
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

This public repository hosts the terminal TUI release packages and user-facing documentation. The latest release is **v1.3.43**, published on **2026-06-11 UTC**. For the graphical desktop app (GUI), use the official downloads page: <https://acosmi.com/zh/downloads>.

### Current Release

| Platform | Architecture | Asset |
|---|---:|---|
| macOS Apple Silicon | arm64 | `crabcode-1.3.43-darwin-arm64.tar.gz` |
| macOS Intel | x64 | `crabcode-1.3.43-darwin-x64.tar.gz` |
| Linux | arm64 | `crabcode-1.3.43-linux-arm64.tar.gz` |
| Linux | x64 | `crabcode-1.3.43-linux-x64.tar.gz` |
| Windows | x64 | `crabcode-1.3.43-win-x64.zip` |

All packages are available on the [latest release](https://github.com/acosmi/crabcode/releases/latest) page with SHA-256 checksum files.

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

**macOS / Linux** — one command (auto-detects platform, fail-closed SHA256 verification, sets up PATH automatically):

```bash
curl -fsSL https://updates.acosmi.com/crabcode/install.sh | sh
```

**Windows** — run in **PowerShell** (not CMD; the prompt should start with `PS `):

```powershell
irm https://updates.acosmi.com/crabcode/install.ps1 | iex
```

Notes:

- The default source is our distribution mirror (`updates.acosmi.com`) with automatic fallback to GitHub Releases. Checksums are fetched from the **same source** as the artifact and verification is fail-closed.
- You can also install straight from GitHub — fully equivalent:

```bash
curl -fsSL https://github.com/acosmi/crabcode/releases/latest/download/install.sh | sh
```

- On Windows, run the interactive TUI from **Windows Terminal** or a modern PowerShell window started in a regular user directory (e.g. `C:\Users\you>`). Legacy CMD windows (especially elevated `C:\Windows\System32>`) may show a frozen or black screen; if you must use legacy CMD, run `chcp 65001` first and disable legacy console mode.
- Manual install (advanced): download the platform archive from [Releases](https://github.com/acosmi/crabcode/releases/latest), extract it, and add the directory to PATH. Keep the directory **intact** — the launcher resolves `dist/`, `bun`, `node_modules/`, and the orchestrator from its own directory; do not copy out a single binary or symlink across directories.

#### Update

Already installed? One command updates to the latest version (replaces program files only — your config, login state, history and memory data are untouched):

```bash
crabcode update
```

You can also type `/update` inside the TUI, or simply re-run the install one-liner above.

#### Windows GUI Edition

Windows users who prefer a graphical app can download the installer directly — no command line or PATH setup needed:

1. Open the [latest release](https://github.com/acosmi/crabcode/releases/latest) and download `crabcode-1.3.43-win-x64-setup.exe` from Assets.
2. Double-click the installer and follow the wizard; launch CrabCode from the Start menu afterwards.

Direct download: <https://github.com/acosmi/crabcode/releases/download/v1.3.43/crabcode-1.3.43-win-x64-setup.exe>

> For the macOS / Linux GUI, use the official downloads page: <https://acosmi.com/zh/downloads>.

### Verify File Integrity

Run this in the directory where you downloaded the release packages:

```bash
curl -fsSL -O https://github.com/acosmi/crabcode/releases/download/v1.3.43/checksums-sha256.txt
shasum -a 256 -c checksums-sha256.txt
```

On Linux you can also use:

```bash
sha256sum -c checksums-sha256.txt
```

For Windows:

```powershell
Invoke-WebRequest `
  -Uri "https://github.com/acosmi/crabcode/releases/download/v1.3.43/checksums-sha256.txt" `
  -OutFile checksums-sha256.txt

$Expected = (Select-String -Path checksums-sha256.txt -Pattern "crabcode-1.3.43-win-x64.zip").Line.Split()[0].ToLower()
$Actual = (Get-FileHash crabcode-1.3.43-win-x64.zip -Algorithm SHA256).Hash.ToLower()
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
