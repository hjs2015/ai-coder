# 🦞 OpenClaw 官方文档完全指南

> **来源**: OpenClaw 官方文档 https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **Discord**: https://discord.com/invite/clawd  
> **许可证**: MIT  
> **提取日期**: 2026-03-22  
> **文档版本**: 官方文档提取版 v2.0（完整版）

---

## 📑 完整目录

### 第一部分：入门指南
- [什么是 OpenClaw](#什么是-openclaw)
- [工作原理](#工作原理)
- [关键功能](#关键功能)
- [快速开始](#快速开始)
- [安装要求](#安装要求)
- [Onboarding 概述](#onboarding-概述)

### 第二部分：安装与配置
- [CLI Onboarding](#cli-onboarding)
- [macOS App Onboarding](#macos-app-onboarding)
- [配置参考](#配置参考)
- [模型配置](#模型配置)

### 第三部分：渠道配置
- [支持的渠道列表](#支持的渠道列表)
- [Telegram 配置](#telegram-配置)
- [WhatsApp 配置](#whatsapp-配置)
- [Discord 配置](#discord-配置)
- [iMessage 配置](#imessage-配置)
- [渠道路由](#渠道路由)

### 第四部分：Agent 与工具
- [Agent 工作区](#agent-工作区)
- [Agent 循环](#agent-循环)
- [子 Agent](#子-agent)
- [工具与插件](#工具与插件)

### 第五部分：模型提供商
- [模型选择](#模型选择)
- [支持的提供商](#支持的提供商)
- [模型故障转移](#模型故障转移)
- [Token 使用与成本](#token-使用与成本)

### 第六部分：参考文档
- [CLI 参考](#cli-参考)
- [RPC 和 API](#rpc-和-api)
- [配置模板](#配置模板)
- [故障排查](#故障排查)

---

## 什么是 OpenClaw

**OpenClaw** 是一个**自托管网关**，将任何聊天应用连接到 AI Agent。

> "EXFOLIATE! EXFOLIATE!" — A space lobster, probably

### 核心定位

任何操作系统的 AI Agent 网关，支持：
- WhatsApp
- Telegram
- Discord
- iMessage
- 以及更多...

从口袋发送消息，获取 Agent 响应。插件支持 Mattermost 和更多渠道。

### 适用场景

- **个人 AI 助理** - 从任何聊天应用访问
- **开发工作流** - 代码审查、调试、生成
- **团队协作** - 多 Agent 协作
- **自动化任务** - 定时任务、监控、通知

---

## 工作原理

```
┌──────────────────┐
│  Chat Apps       │
│  + Plugins       │
└─────────────────┘
         │
         ↓
┌──────────────────┐
│    Gateway       │
│   (OpenClaw)     │
└────────┬─────────┘
         │
    ┌────┴────┬─────────┬──────────┐
    ↓         ↓         ↓          ↓
┌──────┐ ┌────── ┌────────┐ ┌─────────┐
│PI    │ │ CLI  │ │Web UI  │ │Mobile   │
│agent │ │      │ │        │ │nodes    │
└────── └──────┘ └────────┘ └─────────┘
```

**网关是所有会话、路由和渠道连接的单一事实来源。**

---

## 关键功能

### 🚀 多渠道网关
- WhatsApp、Telegram、Discord、iMessage 通过单个网关进程
- 插件支持 Mattermost 和更多

### 🔄 多 Agent 路由
- 每个 Agent、工作区或发送者的隔离会话
- 并行处理多个请求

### 📎 媒体支持
- 发送和接收图片
- 音频消息
- 文档文件

### 🖥️ Web 控制 UI
- 浏览器仪表板
- 聊天界面
- 配置管理
- 会话查看
- 节点管理

### 📱 移动节点
- iOS 节点配对
- Android 节点配对
- Canvas 支持
- 相机集成
- 语音工作流

### 🔌 插件系统
- 扩展渠道支持
- 自定义工具
- Skills 集成

---

## 快速开始

### 3 步安装（5 分钟）

#### 1. 安装 OpenClaw

```bash
npm install -g openclaw@latest
```

#### 2. Onboarding 并安装服务

```bash
openclaw onboard --install-daemon
```

#### 3. 聊天

打开浏览器 Control UI：

```bash
openclaw dashboard
```

或者连接渠道（**Telegram 最快**）并从手机聊天。

---

## 安装要求

### 系统要求

| 组件 | 要求 | 备注 |
|------|------|------|
| **Node.js** | 24 推荐（22.16+ 支持） | 检查：`node --version` |
| **npm** | 最新版 | 随 Node.js 安装 |
| **操作系统** | macOS / Linux / Windows | Windows 支持原生和 WSL2 |

### API Key

需要模型提供商的 API Key：
- Anthropic (Claude)
- OpenAI (GPT)
- Google (Gemini)
- 以及其他 30+ 提供商

Onboarding 过程会提示输入。

### 网络要求

- 互联网连接（用于 API 调用）
- 端口 18789（默认 Dashboard 端口）

---

## Onboarding 概述

OpenClaw 有两个 Onboarding 路径，都配置认证、网关和可选渠道——区别在于交互方式。

### 选择指南

| 特性 | CLI Onboarding | macOS App Onboarding |
|------|---------------|---------------------|
| **平台** | macOS, Linux, Windows | macOS only |
| **界面** | 终端向导 | 应用内引导 UI |
| **最佳场景** | 服务器、无头、完全控制 | 桌面用户、图形界面偏好 |

### CLI Onboarding

**适用**：服务器、无头环境、需要完全控制

```bash
openclaw onboard
```

**配置内容**：
- 模型提供商 API Key
- 网关设置
- 渠道连接
- 服务安装

### macOS App Onboarding

**适用**：macOS 桌面用户

- 图形界面引导
- 一键配置
- 自动安装

---

## CLI Onboarding 详细步骤

### 运行 Onboarding

```bash
openclaw onboard
```

### 配置步骤

1. **选择模型提供商**
   - Anthropic
   - OpenAI
   - Google
   - 其他

2. **输入 API Key**
   - 安全存储到本地配置
   - 不会上传到远程服务器

3. **选择渠道**
   - Telegram（推荐，最简单）
   - WhatsApp
   - Discord
   - iMessage（需要 macOS）
   - 跳过（稍后配置）

4. **安装服务**
   - 系统服务（systemd/launchd）
   - 开机自启
   - 后台运行

### 验证安装

```bash
# 检查状态
openclaw status

# 查看日志
openclaw logs

# 打开 Dashboard
openclaw dashboard
```

---

## 配置参考

### 配置文件位置

```
~/.openclaw/openclaw.json
```

### 默认行为

- **不配置**：使用捆绑的 Pi 二进制文件，RPC 模式，每发送者会话
- **基础配置**：从 `channels.whatsapp.allowFrom` 开始

### 配置示例

```json
{
  "channels": {
    "whatsapp": {
      "allowFrom": ["+15555550123"],
      "groups": {
        "*": { "requireMention": true }
      }
    },
    "messages": {
      "groupChat": {
        "mentionPatterns": ["@openclaw"]
      }
    }
  },
  "models": {
    "default": "claude-sonnet-4-20250514",
    "providers": {
      "anthropic": {
        "apiKey": "sk-ant-xxx"
      }
    }
  }
}
```

### 访问控制

- `allowFrom` - 允许的发送者列表
- `requireMention` - 群组中要求 @提及
- `mentionPatterns` - 提及模式匹配

---

## 模型配置

### 模型选择工作原理

- Onboarding 设置默认模型
- 可通过配置切换
- 支持多模型故障转移

### 快速模型策略

```bash
# 查看当前模型
openclaw models list

# 切换模型
openclaw models set claude-sonnet-4-20250514

# 测试模型
openclaw models test
```

### 配置键（概览）

```json
{
  "models": {
    "default": "模型名称",
    "providers": {
      "提供商名称": {
        "apiKey": "密钥",
        "baseUrl": "可选的自定义 URL"
      }
    }
  }
}
```

### "Model is not allowed" 错误

如果回复停止，可能是：
1. API Key 无效
2. 模型名称错误
3. 账户额度不足

**解决**：重新运行 `openclaw onboard`

---

## 支持的渠道列表

### 消息平台（30+）

| 渠道 | 状态 | 配置难度 |
|------|------|---------|
| **Telegram** | ✅ 生产就绪 | ⭐ 最简单 |
| **WhatsApp** | ✅ 生产就绪 | ⭐⭐ 中等 |
| **Discord** | ✅ 生产就绪 | ⭐⭐ 中等 |
| **iMessage** | ✅ 通过 BlueBubbles | ⭐⭐⭐ 需 macOS |
| **Signal** | ✅ 支持 | ⭐⭐ 中等 |
| **Slack** | ✅ 支持 | ⭐⭐ 中等 |
| **Microsoft Teams** | ✅ 支持 | ⭐⭐⭐ 复杂 |
| **Google Chat** | ✅ 支持 | ⭐⭐ 中等 |
| **Matrix** | ✅ 支持 | ⭐⭐ 中等 |
| **Mattermost** | 🔌 插件 | 需扩展包 |
| **IRC** | ✅ 支持 | ⭐ 简单 |
| **LINE** | ✅ 支持 | ⭐⭐ 中等 |
| **Feishu（飞书）** | ✅ 支持 | ⭐⭐ 中等 |
| **Nextcloud Talk** | ✅ 支持 | ⭐⭐ 中等 |
| **Synology Chat** | ✅ 支持 | ⭐⭐ 中等 |
| **Zalo** | ✅ 支持 | ⭐⭐ 中等 |
| **Nostr** | ✅ 支持 | ⭐⭐ 中等 |
| **Tlon** | ✅ 支持 | ⭐⭐ 中等 |
| **Twitch** | ✅ 支持 | ⭐⭐ 中等 |

### 特殊渠道

- **Voice Call Plugin** - 语音通话
- **BlueBubbles** - iMessage 推荐方案

---

## Telegram 配置

### 快速设置

**状态**：生产就绪，支持机器人私聊和群组

**模式**：Long polling（默认），支持 Webhook

### Telegram 端设置

1. **创建机器人**
   - 联系 @BotFather
   - 发送 `/newbot`
   - 获取 Token

2. **配置 Bot Token**
   ```json
   {
     "channels": {
       "telegram": {
         "botToken": "YOUR_BOT_TOKEN"
       }
     }
   }
   ```

3. **启动对话**
   - 在 Telegram 中搜索机器人
   - 发送 `/start`

### 访问控制和激活

- **私聊**：默认允许
- **群组**：需要配置 `allowGroups`
- **频道**：需要添加为管理员

### 查找 Telegram 用户 ID

```bash
# 方法 1：通过 bot
发送消息给 @userinfobot

# 方法 2：查看日志
openclaw logs | grep "user_id"
```

### 运行时行为

- 自动回复私聊
- 群组中需要 @提及（可配置）
- 支持媒体消息
- 支持回复线程

### 功能参考

| 功能 | 支持 |
|------|------|
| 文本消息 | ✅ |
| 图片 | ✅ |
| 音频 | ✅ |
| 视频 | ✅ |
| 文档 | ✅ |
| 语音消息 | ✅ |
| 回复线程 | ✅ |
| 群组消息 | ✅ |
| 频道消息 | ✅ |

### 故障排查

**问题**：机器人无响应

**解决**：
1. 检查 Bot Token 是否正确
2. 验证网络连接
3. 查看日志：`openclaw logs`

**问题**：群组中无响应

**解决**：
1. 添加机器人为管理员
2. 配置 `allowGroups`
3. 检查隐私设置

---

## WhatsApp 配置

### 配置方式

- 通过 QR 码配对
- 支持个人和群组
- 媒体消息支持

### 快速设置

```json
{
  "channels": {
    "whatsapp": {
      "allowFrom": ["+15555550123"],
      "groups": {
        "*": { "requireMention": true }
      }
    }
  }
}
```

---

## Discord 配置

### 配置步骤

1. 创建 Discord 应用
2. 获取 Bot Token
3. 邀请到服务器
4. 配置渠道

---

## iMessage 配置

### 推荐方案：BlueBubbles

**要求**：
- macOS 服务器
- BlueBubbles 应用
- REST API 访问

### 配置

```json
{
  "channels": {
    "bluebubbles": {
      "serverUrl": "http://your-mac:1234",
      "password": "your-password"
    }
  }
}
```

---

## 渠道路由

### 路由规则

```json
{
  "routing": {
    "rules": [
      {
        "channel": "telegram",
        "pattern": ".*代码.*",
        "agent": "coding-agent"
      },
      {
        "channel": "whatsapp",
        "pattern": ".*天气.*",
        "agent": "weather-agent"
      }
    ]
  }
}
```

### 群组消息

- 支持群组聊天
- 可配置提及要求
- 广播群组支持

---

## Agent 工作区

### 工作区隔离

- 每个工作区独立会话
- 独立配置
- 独立记忆

### 多 Agent 协作

- 主 Agent 协调
- 子 Agent 执行专项任务
- 结果聚合

---

## Agent 循环

### 工具循环检测

- 防止无限循环
- 最大迭代次数配置
- 超时处理

---

## 子 Agent

### 专项 Agent

- 代码审查 Agent
- 测试生成 Agent
- 文档编写 Agent
- Bug 调试 Agent

---

## 工具与插件

### 内置工具

- 文件读写
- 命令执行
- 网络请求
- 代码运行

### 插件系统

- 扩展渠道
- 自定义工具
- Skills 集成

---

## 模型提供商

### 支持的提供商（30+）

#### 主流提供商

| 提供商 | 模型 | 状态 |
|--------|------|------|
| **Anthropic** | Claude Sonnet/Opus | ✅ |
| **OpenAI** | GPT-4/GPT-5 | ✅ |
| **Google** | Gemini | ✅ |
| **xAI** | Grok | ✅ |

#### 中国提供商

| 提供商 | 模型 | 状态 |
|--------|------|------|
| **阿里** | Qwen（通义千问） | ✅ |
| **百度** | Qianfan（文心一言） | ✅ |
| **智谱** | GLM | ✅ |
| **月之暗面** | Moonshot（Kimi） | ✅ |
| **MiniMax** | MiniMax | ✅ |
| **火山引擎** | Doubao（豆包） | ✅ |
| **Z.AI** | Zhipu | ✅ |

#### 其他提供商

- **Amazon Bedrock**
- **Cloudflare AI Gateway**
- **Deepgram**
- **GitHub Copilot**
- **Groq**
- **Hugging Face**
- **Kilo Gateway**
- **LiteLLM**
- **Mistral**
- **NVIDIA**
- **Ollama**（本地模型）
- **OpenRouter**
- **Perplexity**
- **SGLang**
- **Together AI**
- **Vercel AI Gateway**
- **Venice AI**
- **vLLM**
- **Xiaomi MiMo**

---

## 模型故障转移

### 配置故障转移

```json
{
  "models": {
    "failover": [
      "claude-sonnet-4-20250514",
      "gpt-4-turbo",
      "gemini-pro"
    ]
  }
}
```

### 故障转移策略

1. 主模型失败
2. 自动切换到备用模型
3. 记录故障事件

---

## Token 使用与成本

### Token 计算

- 输入 Token：提示词长度
- 输出 Token：回复长度
- 总计：输入 + 输出

### 成本优化

- 使用提示词缓存
- 选择合适模型
- 限制回复长度

---

## CLI 参考

### 基本命令

```bash
# 启动网关
openclaw start

# 停止网关
openclaw stop

# 查看状态
openclaw status

# 打开 Dashboard
openclaw dashboard

# 运行 Onboarding
openclaw onboard

# 查看日志
openclaw logs
```

### 模型命令

```bash
# 列出模型
openclaw models list

# 设置模型
openclaw models set <model-name>

# 测试模型
openclaw models test
```

### 渠道命令

```bash
# 列出渠道
openclaw channels list

# 连接渠道
openclaw channels connect <channel>

# 断开渠道
openclaw channels disconnect <channel>
```

### 配置命令

```bash
# 导出配置
openclaw config export

# 导入配置
openclaw config import

# 重置配置
openclaw config reset
```

---

## RPC 和 API

### RPC 适配器

- 内部进程通信
- 高性能
- 低延迟

### API 端点

```
GET  /api/status
POST /api/message
GET  /api/sessions
POST /api/config
```

---

## 配置模板

### AGENTS.md 模板

```markdown
# Agent 配置

## 身份
- 名字：Assistant
- 定位：AI 助手

## 能力
- 代码生成
- Bug 调试
- 文档编写
```

### HEARTBEAT.md 模板

```markdown
# Heartbeat 任务

- [ ] 检查系统状态
- [ ] 处理待办事项
- [ ] 生成报告
```

### TOOLS.md 模板

```markdown
# 可用工具

## 文件操作
- 读取文件
- 写入文件
- 删除文件

## 命令执行
- 运行 shell 命令
- 获取输出
```

---

## 故障排查

### 常见问题

#### 1. 端口被占用

**错误**：`Port 18789 is already in use`

**解决**：
```bash
# 查找占用进程
lsof -i :18789

# 杀掉进程
kill -9 <PID>

# 或更改端口
openclaw config set port 18790
```

#### 2. API Key 无效

**错误**：`Invalid API key`

**解决**：
- 检查 API Key 是否正确
- 确认账户有额度
- 重新运行 onboarding

#### 3. 渠道连接失败

**错误**：`Failed to connect to channel`

**解决**：
- 检查网络连接
- 验证渠道凭证
- 查看日志

#### 4. 模型不允许

**错误**：`Model is not allowed`

**解决**：
- 检查模型名称
- 验证提供商配置
- 重新运行 onboarding

#### 5. 工具循环检测

**错误**：`Tool loop detected`

**解决**：
- 检查工具调用逻辑
- 增加最大迭代次数
- 优化 Agent 提示词

---

## 高级配置

### 环境变量

```bash
# 模型配置
export OPENCLAW_MODEL=claude-sonnet-4-20250514
export ANTHROPIC_API_KEY=sk-ant-xxx

# 网关配置
export OPENCLAW_PORT=18789
export OPENCLAW_HOST=0.0.0.0

# 日志级别
export OPENCLAW_LOG_LEVEL=info
```

### 系统服务

#### systemd (Linux)

```ini
[Unit]
Description=OpenClaw Gateway
After=network.target

[Service]
Type=simple
User=youruser
ExecStart=/usr/bin/openclaw start
Restart=always

[Install]
WantedBy=multi-user.target
```

#### Launchd (macOS)

```xml
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
</dict>
</plist>
```

---

## 安全最佳实践

### 1. API Key 保护

- 不提交到 Git
- 使用环境变量
- 定期轮换

### 2. 访问控制

- 配置 `allowFrom`
- 群组要求 @提及
- IP 白名单

### 3. 数据隐私

- 自托管确保控制
- 本地存储会话
- 不依赖第三方

---

## 资源链接

### 官方资源
- **官网**: https://openclaw.ai/
- **文档**: https://docs.openclaw.ai/
- **GitHub**: https://github.com/openclaw/openclaw
- **Discord**: https://discord.com/invite/clawd
- **Releases**: https://github.com/openclaw/openclaw/releases

### 社区资源
- **Discord 社区**: 用户论坛
- **GitHub Issues**: 问题反馈
- **插件市场**: （即将推出）

---

## 贡献指南

### 开发环境

```bash
# 克隆仓库
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 开发模式
npm run dev
```

### 提交代码

1. Fork 仓库
2. 创建分支
3. 提交更改
4. 创建 PR

---

## 许可证

**MIT License**

允许免费使用、复制、修改、合并、出版、发行、再授权。

---

## 致谢

感谢所有贡献者和社区成员！

**"EXFOLIATE! EXFOLIATE!"** — A space lobster, probably

---

**文档版本**: 官方文档提取版 v2.0（完整版）  
**最后更新**: 2026-03-22  
**内容来源**: https://docs.openclaw.ai/  
**提取方式**: 官方文档逐页面获取整理
