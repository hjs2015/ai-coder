# 🦞 OpenClaw 完全指南 - AI 聊天网关

> **官方文档**: https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **Discord**: https://discord.com/invite/clawd  
> **许可证**: MIT  
> **文档版本**: v2.0 全面优化版  
> **最后更新**: 2026-03-23  

---

## 📖 完整目录

### 第 0 部分 快速开始（5 分钟上手）
- [0.1 什么是 OpenClaw](#01-什么是-openclaw)
- [0.2 核心特性](#02-核心特性)
- [0.3 快速安装](#03-快速安装)
- [0.4 首次使用](#04-首次使用)

### 第 1 部分 安装与部署
- [1.1 系统要求](#11-系统要求)
- [1.2 安装方法对比](#12-安装方法对比)
- [1.3 macOS/Linux 安装](#13-macoslinux-安装)
- [1.4 Windows 安装](#14-windows-安装)
- [1.5 Docker 安装](#15-docker-安装)
- [1.6 源码安装](#16-源码安装)

### 第 2 部分 Onboarding 引导
- [2.1 Onboarding 概述](#21-onboarding-概述)
- [2.2 CLI Onboarding](#22-cli-onboarding)
- [2.3 macOS App Onboarding](#23-macos-app-onboarding)
- [2.4 自定义 Provider](#24-自定义-provider)

### 第 3 部分 渠道配置
- [3.1 渠道概述](#31-渠道概述)
- [3.2 Telegram 配置](#32-telegram-配置)
- [3.3 WhatsApp 配置](#33-whatsapp-配置)
- [3.4 Discord 配置](#34-discord-配置)
- [3.5 iMessage 配置](#35-imessage-配置)
- [3.6 其他渠道](#36-其他渠道)

### 第 4 部分 模型配置
- [4.1 支持的模型](#41-支持的模型)
- [4.2 Anthropic Claude](#42-anthropic-claude)
- [4.3 OpenAI GPT](#43-openai-gpt)
- [4.4 Google Gemini](#44-google-gemini)
- [4.5 本地模型](#45-本地模型)

### 第 5 部分 配置详解
- [5.1 配置文件结构](#51-配置文件结构)
- [5.2 网关配置](#52-网关配置)
- [5.3 渠道配置](#53-渠道配置)
- [5.4 Agent 配置](#54-agent-配置)
- [5.5 环境变量](#55-环境变量)

### 第 6 部分 使用指南
- [6.1 Dashboard 使用](#61-dashboard-使用)
- [6.2 个人助理设置](#62-个人助理设置)
- [6.3 多 Agent 路由](#63-多-agent-路由)
- [6.4 移动节点配对](#64-移动节点配对)

### 第 7 部分 CLI 参考
- [7.1 基本命令](#71-基本命令)
- [7.2 网关命令](#72-网关命令)
- [7.3 渠道命令](#73-渠道命令)
- [7.4 配置命令](#74-配置命令)

### 第 8 部分 自动化与脚本
- [8.1 CLI 自动化](#81-cli-自动化)
- [8.2 系统服务](#82-系统服务)
- [8.3 API 调用](#83-api-调用)

### 第 9 部分 故障排查
- [9.1 常见问题](#91-常见问题)
- [9.2 日志分析](#92-日志分析)
- [9.3 性能优化](#93-性能优化)

### 第 10 部分 最佳实践
- [10.1 安全配置](#101-安全配置)
- [10.2 生产部署](#102-生产部署)
- [10.3 备份恢复](#103-备份恢复)

---

## 第 0 部分 快速开始（5 分钟上手）

### 0.1 什么是 OpenClaw

**OpenClaw** 是一个**自托管网关**，将您最喜欢的聊天应用连接到 AI 编码 Agent。

```
┌─────────────────┐
│  聊天应用        │
│  WhatsApp       │
│  Telegram       │
│  Discord        │
│  iMessage       │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│   OpenClaw      │
│    Gateway      │
└────────────────┘
         │
    ┌────┴────┬────────┐
    ↓         ↓        ↓
┌──────┐ ┌──────┐ ┌────────┐
│  Pi  │ │ CLI  │ │  Web   │
│Agent │ │      │ │   UI   │
└──────┘ └──────┘ └────────┘
```

**适用人群**:
- 开发者想要个人 AI 助理
- 需要从任何地方发送消息
- 不想依赖托管服务
- 希望完全控制数据

### 0.2 核心特性

| 特性 | 说明 |
|------|------|
| **自托管** | 运行在您的硬件，您的规则 |
| **多渠道** | 一个网关服务 WhatsApp、Telegram、Discord 等 |
| **Agent 原生** | 为编码 Agent 构建，支持工具使用、会话、记忆 |
| **多 Agent 路由** | 隔离会话，工作区分隔 |
| **媒体支持** | 发送和接收图片、音频、文档 |
| **移动节点** | 配对 iOS 和 Android 设备 |
| **开源** | MIT 许可，社区驱动 |

### 0.3 快速安装

#### 方法 1：一键安装脚本（推荐）

**macOS / Linux**:
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Windows (PowerShell)**:
```powershell
irm https://openclaw.ai/install.sh | iex
```

#### 方法 2：npm 安装

```bash
npm install -g openclaw@latest
```

#### 方法 3：Docker

```bash
docker run -d \
  --name openclaw \
  -p 18789:18789 \
  -v ~/.openclaw:/root/.openclaw \
  ghcr.io/openclaw/openclaw:latest
```

### 0.4 首次使用

#### 步骤 1：运行 Onboarding

```bash
openclaw onboard --install-daemon
```

向导会引导您：
1. 选择模型提供商（Anthropic/OpenAI/Google）
2. 输入 API Key
3. 配置网关端口
4. 安装后台服务

#### 步骤 2：验证运行状态

```bash
openclaw gateway status
```

应该看到网关监听在端口 18789。

#### 步骤 3：打开 Dashboard

```bash
openclaw dashboard
```

这会在浏览器中打开 Control UI。

#### 步骤 4：发送第一条消息

在 Control UI 聊天框中输入：
```
你好，请介绍一下自己
```

#### 步骤 5：连接手机渠道（可选）

最快的渠道是 **Telegram**：
```bash
openclaw channels add telegram
```

按照提示输入 Bot Token。

---

## 第 1 部分 安装与部署

### 1.1 系统要求

#### 硬件要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| **CPU** | 双核 | 四核+ |
| **内存** | 2GB | 4GB+ |
| **磁盘** | 1GB | 5GB+ SSD |
| **网络** | 宽带连接 | 稳定宽带 |

#### 软件要求

| 组件 | 版本要求 | 说明 |
|------|---------|------|
| **Node.js** | 22.16+ | 推荐 Node 24 |
| **npm** | 10+ | 随 Node.js 安装 |
| **操作系统** | Windows 10+/macOS 12+/Linux | 支持主流系统 |

**检查 Node 版本**:
```bash
node --version
```

### 1.2 安装方法对比

| 方法 | 适用场景 | 优点 | 缺点 |
|------|---------|------|------|
| **安装脚本** | 新手/快速开始 | 一键安装，自动配置 | 自定义性低 |
| **npm** | 开发者 | 标准方式，易更新 | 需 Node 环境 |
| **Docker** | 生产环境 | 隔离性好，易迁移 | 需 Docker 知识 |
| **源码** | 贡献者/定制 | 完全控制 | 复杂，需编译 |

### 1.3 macOS/Linux 安装

#### 使用安装脚本

```bash
# 下载安装脚本
curl -fsSL https://openclaw.ai/install.sh -o install.sh

# 执行安装
bash install.sh

# 验证安装
openclaw --version
```

#### 使用 npm

```bash
# 全局安装
npm install -g openclaw@latest

# 验证
openclaw --version

# 查看帮助
openclaw --help
```

#### 卸载

```bash
# npm 安装的用 npm 卸载
npm uninstall -g openclaw

# 清理配置（可选）
rm -rf ~/.openclaw
```

### 1.4 Windows 安装

#### 使用 PowerShell 脚本

```powershell
# 下载安装脚本
irm https://openclaw.ai/install.sh -o install.ps1

# 执行安装
.\install.ps1

# 验证
openclaw --version
```

#### WSL2 安装（推荐）

```bash
# 在 WSL2 中安装
curl -fsSL https://openclaw.ai/install.sh | bash

# 验证
openclaw --version
```

**WSL2 优势**:
- 更好的稳定性
- 与 Linux 环境一致
- 更完整的特性支持

### 1.5 Docker 安装

#### 基本安装

```bash
# 拉取镜像
docker pull ghcr.io/openclaw/openclaw:latest

# 运行容器
docker run -d \
  --name openclaw \
  -p 18789:18789 \
  -v ~/.openclaw:/root/.openclaw \
  --restart unless-stopped \
  ghcr.io/openclaw/openclaw:latest
```

#### Docker Compose

```yaml
version: '3.8'

services:
  openclaw:
    image: ghcr.io/openclaw/openclaw:latest
    container_name: openclaw
    ports:
      - "18789:18789"
    volumes:
      - ~/.openclaw:/root/.openclaw
    environment:
      - OPENCLAW_PORT=18789
      - OPENCLAW_HOST=0.0.0.0
    restart: unless-stopped
```

```bash
# 启动
docker-compose up -d

# 查看日志
docker-compose logs -f openclaw

# 停止
docker-compose down
```

### 1.6 源码安装

```bash
# 克隆仓库
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 构建
npm run build

# 全局链接
npm link

# 验证
openclaw --version
```

---

## 第 2 部分 Onboarding 引导

### 2.1 Onboarding 概述

OpenClaw 提供两种 Onboarding 路径：

| 路径 | 平台 | 界面 | 适用场景 |
|------|------|------|---------|
| **CLI** | macOS/Linux/Windows | 终端向导 | 服务器、无头、完全控制 |
| **macOS App** | macOS only | 图形界面 | 桌面 Mac、可视化设置 |

**大多数用户应该从 CLI Onboarding 开始** - 它适用于所有平台并提供最多控制。

### 2.2 CLI Onboarding

#### 基本命令

```bash
# 运行 Onboarding
openclaw onboard

# 同时安装后台服务
openclaw onboard --install-daemon

# 非交互模式（脚本用）
openclaw onboard --non-interactive
```

#### Onboarding 配置内容

1. **模型提供商和认证**
   - API Key、OAuth 或访问令牌
   - 选择提供商（Anthropic/OpenAI/Google）

2. **工作区**
   - Agent 文件目录
   - 引导模板
   - 记忆存储

3. **网关**
   - 端口（默认 18789）
   - 绑定地址
   - 认证模式

4. **渠道**（可选）
   - WhatsApp、Telegram、Discord 等

5. **守护进程**（可选）
   - 后台服务，自动启动

#### Onboarding 流程示例

```bash
$ openclaw onboard

🦞 OpenClaw Onboarding Wizard

? Choose your model provider:
  ❯ Anthropic (Claude)
    OpenAI (GPT)
    Google (Gemini)
    Custom Provider

? Enter your Anthropic API Key: sk-ant-...

? Gateway port (default: 18789): 18789

? Install as background service? Yes

✅ Onboarding complete!
✅ Gateway installed and running
✅ Dashboard: http://127.0.0.1:18789
```

### 2.3 macOS App Onboarding

1. **下载 App**
   ```bash
   # 从 GitHub Releases 下载
   # https://github.com/openclaw/openclaw/releases
   ```

2. **打开 App**
   - 首次运行会启动向导
   - 图形界面引导配置

3. **配置步骤**
   - 选择模型提供商
   - 输入 API Key
   - 选择渠道
   - 完成设置

### 2.4 自定义 Provider

如果您的提供商不在 Onboarding 列表中：

```bash
openclaw onboard --custom-provider
```

**需要配置**:
- API 兼容模式（OpenAI 兼容、Anthropic 兼容、自动检测）
- Base URL 和 API Key
- 模型 ID 和可选别名

**示例**:
```json
{
  "providers": {
    "custom-1": {
      "name": "My Custom Provider",
      "compatibility": "openai",
      "baseUrl": "https://api.myprovider.com/v1",
      "apiKey": "sk-xxx",
      "models": ["model-1", "model-2"]
    }
  }
}
```

---

## 第 3 部分 渠道配置

### 3.1 渠道概述

OpenClaw 支持多种聊天渠道：

| 渠道 | 状态 | 设置难度 | 速度 |
|------|------|---------|------|
| **Telegram** | ✅ 内置 | ⭐ 最简单 | 快 |
| **WhatsApp** | ✅ 内置 | ⭐⭐ 中等 | 快 |
| **Discord** | ✅ 内置 | ⭐⭐ 中等 | 快 |
| **iMessage** | ✅ 内置 | ⭐⭐⭐ 需 macOS | 快 |
| **Mattermost** | 🔌 插件 | ⭐⭐ 中等 | 快 |

### 3.2 Telegram 配置

**最快的渠道** - 只需 Bot Token

#### 步骤 1：创建 Bot

1. 在 Telegram 中搜索 `@BotFather`
2. 发送 `/newbot`
3. 按照提示设置 Bot 名称
4. 获取 Bot Token

#### 步骤 2：添加渠道

```bash
openclaw channels add telegram
```

#### 步骤 3：输入 Token

```
? Enter your Telegram Bot Token: 123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11

✅ Telegram channel added!
✅ Bot connected
```

#### 步骤 4：测试

在 Telegram 中给 Bot 发送消息，应该收到 AI 回复。

### 3.3 WhatsApp 配置

#### 使用 WhatsApp Cloud API

**步骤 1：创建 Meta 开发者账号**
- 访问 https://developers.facebook.com/
- 创建应用

**步骤 2：获取凭证**
- Phone Number ID
- Access Token
- Business Account ID

**步骤 3：添加渠道**
```bash
openclaw channels add whatsapp
```

**步骤 4：配置**
```json
{
  "channels": {
    "whatsapp": {
      "phoneNumberId": "123456789",
      "accessToken": "EAAB...",
      "businessAccountId": "987654321"
    }
  }
}
```

### 3.4 Discord 配置

#### 步骤 1：创建 Discord 应用

1. 访问 https://discord.com/developers/applications
2. 创建新应用
3. 获取 Bot Token

#### 步骤 2：邀请 Bot

```
https://discord.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&permissions=8&scope=bot
```

#### 步骤 3：添加渠道

```bash
openclaw channels add discord
```

### 3.5 iMessage 配置

**仅支持 macOS**

#### 要求
- macOS 12+
- 启用辅助功能权限
- iMessage 账号已登录

#### 配置
```bash
openclaw channels add imessage
```

### 3.6 其他渠道

#### Mattermost（插件）

```bash
# 安装插件
openclaw plugins install mattermost

# 配置
openclaw channels add mattermost
```

#### 自定义渠道

通过插件系统可以添加更多渠道。

---

## 第 4 部分 模型配置

### 4.1 支持的模型

| 提供商 | 模型 | 状态 |
|--------|------|------|
| **Anthropic** | Claude 3.5 Sonnet | ✅ |
| **Anthropic** | Claude 3 Opus | ✅ |
| **OpenAI** | GPT-4o | ✅ |
| **OpenAI** | GPT-4 Turbo | ✅ |
| **Google** | Gemini 1.5 Pro | ✅ |
| **Google** | Gemini 1.5 Flash | ✅ |

### 4.2 Anthropic Claude

**推荐用于编码任务**

#### 配置

```bash
openclaw models set anthropic
```

**环境变量**:
```bash
export ANTHROPIC_API_KEY=sk-ant-xxx
export OPENCLAW_MODEL=claude-sonnet-4-20250514
```

**配置文件**:
```json
{
  "models": {
    "default": "claude-sonnet-4-20250514",
    "anthropic": {
      "apiKey": "sk-ant-xxx",
      "models": [
        "claude-sonnet-4-20250514",
        "claude-opus-20241022"
      ]
    }
  }
}
```

### 4.3 OpenAI GPT

#### 配置

```bash
openclaw models set openai
```

**环境变量**:
```bash
export OPENAI_API_KEY=sk-xxx
export OPENCLAW_MODEL=gpt-4o
```

### 4.4 Google Gemini

#### 配置

```bash
openclaw models set google
```

**环境变量**:
```bash
export GOOGLE_API_KEY=xxx
export OPENCLAW_MODEL=gemini-1.5-pro
```

### 4.5 本地模型

#### Ollama 集成

```bash
# 安装 Ollama
curl -fsSL https://ollama.ai/install.sh | sh

# 拉取模型
ollama pull codellama

# 配置 OpenClaw
openclaw models set ollama
```

**配置**:
```json
{
  "models": {
    "ollama": {
      "baseUrl": "http://localhost:11434",
      "model": "codellama"
    }
  }
}
```

---

## 第 5 部分 配置详解

### 5.1 配置文件结构

配置文件位于 `~/.openclaw/openclaw.json`

```json
{
  "gateway": { ... },
  "models": { ... },
  "channels": { ... },
  "agents": { ... },
  "routing": { ... }
}
```

### 5.2 网关配置

```json
{
  "gateway": {
    "port": 18789,
    "host": "0.0.0.0",
    "auth": {
      "mode": "token",
      "token": "your-auth-token"
    },
    "logging": {
      "level": "info",
      "file": "~/.openclaw/gateway.log"
    }
  }
}
```

### 5.3 渠道配置

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11",
      "allowFrom": ["*"],
      "groups": {
        "*": {
          "requireMention": true
        }
      }
    },
    "whatsapp": {
      "enabled": false,
      "phoneNumberId": "123456789",
      "accessToken": "EAAB...",
      "allowFrom": ["+1234567890"]
    }
  }
}
```

### 5.4 Agent 配置

```json
{
  "agents": {
    "default": {
      "model": "claude-sonnet-4-20250514",
      "systemPrompt": "You are a helpful coding assistant.",
      "tools": ["file_read", "file_write", "shell"],
      "memory": true
    },
    "coding": {
      "model": "claude-sonnet-4-20250514",
      "systemPrompt": "You are an expert programmer.",
      "tools": ["file_read", "file_write", "shell", "git"]
    }
  }
}
```

### 5.5 环境变量

```bash
# 网关配置
export OPENCLAW_PORT=18789
export OPENCLAW_HOST=0.0.0.0

# 模型配置
export ANTHROPIC_API_KEY=sk-ant-xxx
export OPENAI_API_KEY=sk-xxx
export GOOGLE_API_KEY=xxx

# 日志配置
export OPENCLAW_LOG_LEVEL=info
export OPENCLAW_LOG_FILE=~/.openclaw/gateway.log

# 工作区配置
export OPENCLAW_WORKSPACE=~/openclaw-workspace
```

---

## 第 6 部分 使用指南

### 6.1 Dashboard 使用

#### 访问 Dashboard

**本地**:
```
http://127.0.0.1:18789/
```

**远程**:
- 使用 Web surfaces
- 使用 Tailscale

#### Dashboard 功能

1. **聊天界面**
   - 发送消息给 Agent
   - 查看历史会话
   - 管理上下文

2. **配置管理**
   - 修改网关设置
   - 管理渠道
   - 配置模型

3. **会话查看**
   - 活跃会话列表
   - 会话详情
   - 终止会话

4. **节点管理**
   - 查看移动节点
   - 配对新设备
   - 管理节点权限

### 6.2 个人助理设置

#### 步骤 1：选择主要渠道

推荐 Telegram（最简单）

#### 步骤 2：配置个人偏好

```json
{
  "preferences": {
    "language": "zh-CN",
    "timezone": "Asia/Shanghai",
    "responseStyle": "concise"
  }
}
```

#### 步骤 3：设置快捷命令

```json
{
  "shortcuts": {
    "/code": "Help me write code",
    "/debug": "Debug this error",
    "/explain": "Explain this code"
  }
}
```

### 6.3 多 Agent 路由

#### 配置路由规则

```json
{
  "routing": {
    "rules": [
      {
        "pattern": ".*代码.*|.*bug.*|.*错误.*",
        "agent": "coding-agent",
        "priority": 1
      },
      {
        "pattern": ".*天气.*|.*新闻.*",
        "agent": "info-agent",
        "priority": 2
      },
      {
        "pattern": ".*",
        "agent": "default-agent",
        "priority": 99
      }
    ]
  }
}
```

#### 工作区隔离

```json
{
  "workspaces": {
    "work": {
      "agents": ["coding-agent"],
      "channels": ["telegram-work"]
    },
    "personal": {
      "agents": ["personal-agent"],
      "channels": ["whatsapp-personal"]
    }
  }
}
```

### 6.4 移动节点配对

#### iOS 节点

1. **下载 iOS App**
   - 从 App Store 下载 OpenClaw Nodes

2. **配对**
   ```bash
   openclaw nodes pair ios
   ```

3. **扫描二维码**
   - App 会显示二维码
   - 用 Dashboard 扫描

#### Android 节点

1. **下载 Android App**
   - 从 Google Play 下载

2. **配对**
   ```bash
   openclaw nodes pair android
   ```

---

## 第 7 部分 CLI 参考

### 7.1 基本命令

```bash
# 查看版本
openclaw --version

# 查看帮助
openclaw --help

# 启动网关
openclaw start

# 停止网关
openclaw stop

# 重启网关
openclaw restart

# 查看状态
openclaw status
```

### 7.2 网关命令

```bash
# 网关状态
openclaw gateway status

# 网关日志
openclaw gateway logs

# 网关日志（跟随）
openclaw gateway logs -f

# 重启网关
openclaw gateway restart

# 停止网关
openclaw gateway stop
```

### 7.3 渠道命令

```bash
# 列出渠道
openclaw channels list

# 添加渠道
openclaw channels add telegram

# 移除渠道
openclaw channels remove telegram

# 测试渠道
openclaw channels test telegram

# 渠道状态
openclaw channels status telegram
```

### 7.4 配置命令

```bash
# 查看配置
openclaw config show

# 编辑配置
openclaw config edit

# 验证配置
openclaw config validate

# 重置配置
openclaw config reset

# 导出配置
openclaw config export > config.json

# 导入配置
openclaw config import config.json
```

---

## 第 8 部分 自动化与脚本

### 8.1 CLI 自动化

#### 启动脚本

```bash
#!/bin/bash
# start-openclaw.sh

echo "Starting OpenClaw Gateway..."
openclaw start

# 等待网关启动
sleep 5

# 检查状态
if openclaw gateway status | grep -q "running"; then
    echo "✅ Gateway started successfully"
else
    echo "❌ Gateway failed to start"
    exit 1
fi
```

#### 备份脚本

```bash
#!/bin/bash
# backup-openclaw.sh

BACKUP_DIR=~/backups/openclaw
DATE=$(date +%Y%m%d_%H%M%S)

mkdir -p $BACKUP_DIR

# 备份配置
cp -r ~/.openclaw $BACKUP_DIR/openclaw_$DATE

# 压缩
tar -czf $BACKUP_DIR/openclaw_$DATE.tar.gz $BACKUP_DIR/openclaw_$DATE

# 清理旧备份（保留 7 天）
find $BACKUP_DIR -name "openclaw_*.tar.gz" -mtime +7 -delete

echo "✅ Backup completed: openclaw_$DATE.tar.gz"
```

### 8.2 系统服务

#### systemd (Linux)

```ini
# /etc/systemd/system/openclaw.service

[Unit]
Description=OpenClaw Gateway
After=network.target

[Service]
Type=simple
User=youruser
ExecStart=/usr/bin/openclaw start
Restart=always
RestartSec=5
Environment="OPENCLAW_LOG_LEVEL=info"

[Install]
WantedBy=multi-user.target
```

```bash
# 启用服务
sudo systemctl enable openclaw

# 启动服务
sudo systemctl start openclaw

# 查看状态
sudo systemctl status openclaw

# 查看日志
journalctl -u openclaw -f
```

#### Launchd (macOS)

```xml
<!-- ~/Library/LaunchAgents/com.openclaw.gateway.plist -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.openclaw.gateway</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/openclaw</string>
        <string>start</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <true/>
    <key>StandardOutPath</key>
    <string>/tmp/openclaw.log</string>
    <key>StandardErrorPath</key>
    <string>/tmp/openclaw.err</string>
</dict>
</plist>
```

```bash
# 加载服务
launchctl load ~/Library/LaunchAgents/com.openclaw.gateway.plist

# 卸载服务
launchctl unload ~/Library/LaunchAgents/com.openclaw.gateway.plist
```

#### Windows 服务（NSSM）

```bash
# 下载 NSSM
# https://nssm.cc/download

# 安装服务
nssm install OpenClaw "C:\Program Files\nodejs\openclaw.cmd" "start"

# 启动服务
nssm start OpenClaw
```

### 8.3 API 调用

#### 获取会话列表

```bash
curl http://127.0.0.1:18789/api/sessions \
  -H "Authorization: Bearer YOUR_TOKEN"
```

#### 发送消息

```bash
curl http://127.0.0.1:18789/api/chat \
  -X POST \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "Hello",
    "channel": "telegram"
  }'
```

---

## 第 9 部分 故障排查

### 9.1 常见问题

#### 问题 1：端口被占用

**错误**:
```
Error: Port 18789 is already in use
```

**解决**:
```bash
# 查找占用进程
lsof -i :18789  # macOS/Linux
netstat -ano | findstr :18789  # Windows

# 杀掉进程
kill -9 <PID>

# 或更改端口
openclaw config set gateway.port 18790
```

#### 问题 2：API Key 无效

**错误**:
```
Invalid API key
```

**解决**:
1. 检查 API Key 是否正确复制
2. 确认账户有可用额度
3. 重新运行 onboarding

```bash
openclaw onboard
```

#### 问题 3：渠道连接失败

**错误**:
```
Failed to connect to channel
```

**解决**:
1. 检查网络连接
2. 验证渠道凭证
3. 查看日志

```bash
openclaw gateway logs -f
```

#### 问题 4：网关无法启动

**解决**:
```bash
# 查看详细日志
openclaw gateway logs --verbose

# 检查配置
openclaw config validate

# 重置配置
openclaw config reset
openclaw onboard
```

### 9.2 日志分析

#### 查看日志

```bash
# 实时日志
openclaw gateway logs -f

# 最近 100 行
openclaw gateway logs -n 100

# 错误日志
openclaw gateway logs --level error

# 导出日志
openclaw gateway logs > gateway.log
```

#### 日志级别

| 级别 | 说明 | 使用场景 |
|------|------|---------|
| **error** | 错误信息 | 生产环境 |
| **warn** | 警告信息 | 生产环境 |
| **info** | 一般信息 | 默认 |
| **debug** | 调试信息 | 开发调试 |
| **verbose** | 详细信息 | 深度调试 |

#### 常见日志消息

```
[INFO] Gateway started on port 18789
[INFO] Channel telegram connected
[WARN] API rate limit approaching
[ERROR] Failed to connect to model provider
[DEBUG] Processing message from user 123
```

### 9.3 性能优化

#### 内存优化

```json
{
  "gateway": {
    "memory": {
      "maxSessions": 100,
      "sessionTimeout": 3600,
      "cacheSize": 1000
    }
  }
}
```

#### 网络优化

```json
{
  "gateway": {
    "network": {
      "maxConnections": 1000,
      "connectionTimeout": 30000,
      "keepAlive": true
    }
  }
}
```

---

## 第 10 部分 最佳实践

### 10.1 安全配置

#### API Key 保护

```bash
# 使用环境变量
export ANTHROPIC_API_KEY=sk-ant-xxx

# 不要提交到 Git
echo "*.key" >> ~/.openclaw/.gitignore
echo "api_keys.json" >> ~/.openclaw/.gitignore
```

#### 访问控制

```json
{
  "channels": {
    "telegram": {
      "allowFrom": ["+1234567890", "+0987654321"],
      "blockFrom": ["+1111111111"],
      "groups": {
        "*": {
          "requireMention": true,
          "allowedGroups": ["group1", "group2"]
        }
      }
    }
  }
}
```

#### 速率限制

```json
{
  "gateway": {
    "rateLimit": {
      "enabled": true,
      "requestsPerMinute": 60,
      "messagesPerHour": 1000
    }
  }
}
```

### 10.2 生产部署

#### 高可用配置

```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  openclaw-1:
    image: ghcr.io/openclaw/openclaw:latest
    deploy:
      replicas: 2
      resources:
        limits:
          cpus: '2'
          memory: 4G
    volumes:
      - ~/.openclaw:/root/.openclaw
    networks:
      - openclaw-net

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - openclaw-1

networks:
  openclaw-net:
    driver: bridge
```

#### 监控配置

```json
{
  "monitoring": {
    "enabled": true,
    "metrics": {
      "port": 9090,
      "path": "/metrics"
    },
    "healthcheck": {
      "enabled": true,
      "interval": 30
    }
  }
}
```

### 10.3 备份恢复

#### 备份策略

```bash
#!/bin/bash
# backup-strategy.sh

# 每日备份（保留 7 天）
# 每周备份（保留 4 周）
# 每月备份（保留 12 月）

DATE=$(date +%Y%m%d)
WEEK=$(date +%Y-W%V)
MONTH=$(date +%Y%m)

# 每日
cp -r ~/.openclaw ~/backups/daily/openclaw_$DATE

# 每周（周日执行）
if [ $(date +%u) -eq 7 ]; then
    cp -r ~/.openclaw ~/backups/weekly/openclaw_$WEEK
fi

# 每月（1 号执行）
if [ $(date +%d) -eq 01 ]; then
    cp -r ~/.openclaw ~/backups/monthly/openclaw_$MONTH
fi
```

#### 恢复流程

```bash
# 停止网关
openclaw stop

# 备份当前配置
mv ~/.openclaw ~/.openclaw.backup

# 恢复备份
cp -r ~/backups/daily/openclaw_20260322 ~/.openclaw

# 启动网关
openclaw start

# 验证
openclaw gateway status
```

---

## 附录 A：快速参考卡片

### 常用命令

```bash
# 安装
curl -fsSL https://openclaw.ai/install.sh | bash

# Onboarding
openclaw onboard --install-daemon

# 启动/停止
openclaw start
openclaw stop

# 状态
openclaw gateway status

# 日志
openclaw gateway logs -f

# Dashboard
openclaw dashboard

# 添加渠道
openclaw channels add telegram
```

### 配置文件位置

```
~/.openclaw/openclaw.json      # 主配置
~/.openclaw/channels/          # 渠道配置
~/.openclaw/agents/            # Agent 配置
~/.openclaw/logs/              # 日志文件
```

### 默认端口

```
18789 - Gateway HTTP API
18790 - Dashboard (可选)
```

### 环境变量

```bash
OPENCLAW_PORT=18789
OPENCLAW_HOST=0.0.0.0
OPENCLAW_LOG_LEVEL=info
ANTHROPIC_API_KEY=sk-ant-xxx
OPENAI_API_KEY=sk-xxx
GOOGLE_API_KEY=xxx
```

---

## 附录 B：资源链接

### 官方资源
- **官网**: https://openclaw.ai/
- **文档**: https://docs.openclaw.ai/
- **GitHub**: https://github.com/openclaw/openclaw
- **Discord**: https://discord.com/invite/clawd
- **Releases**: https://github.com/openclaw/openclaw/releases

### 社区资源
- **插件市场**: （开发中）
- **用户论坛**: Discord 社区
- **问题反馈**: GitHub Issues

### 学习资源
- **快速开始**: https://docs.openclaw.ai/start/getting-started
- **渠道配置**: https://docs.openclaw.ai/channels
- **模型配置**: https://docs.openclaw.ai/models
- **CLI 参考**: https://docs.openclaw.ai/reference/cli

---

## 附录 C：版本历史

### v2.0 (2026-03-23)
- ✅ 全面优化文档结构
- ✅ 补充官方文档最新内容
- ✅ 添加详细配置示例
- ✅ 完善故障排查章节
- ✅ 添加最佳实践指南

### v1.0 (2026-03-22)
- ✅ 初始版本
- ✅ 基于官方文档提取

---

**文档版本**: v2.0 全面优化版  
**最后更新**: 2026-03-23  
**内容来源**: https://docs.openclaw.ai/ + 实战经验  
**许可证**: MIT（与 OpenClaw 一致）

---

*"EXFOLIATE! EXFOLIATE!" — A space lobster, probably* 🦞
