# 🦞 OpenClaw 官方文档完全指南

> **来源**: OpenClaw 官方文档 https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **Discord**: https://discord.com/invite/clawd  
> **许可证**: MIT  
> **提取日期**: 2026-03-22  
> **文档版本**: 官方文档提取版

---

## 📑 目录

### 第一部分：快速开始
- [什么是 OpenClaw](#什么是-openclaw)
- [工作原理](#工作原理)
- [关键功能](#关键功能)
- [快速开始](#快速开始)
- [Dashboard 控制面板](#dashboard-控制面板)

### 第二部分：安装与配置
- [安装 OpenClaw](#安装-openclaw)
- [Onboarding 引导](#onboarding-引导)
- [配置说明](#配置说明)

### 第三部分：核心概念
- [多渠道网关](#多渠道网关)
- [Agent 路由](#agent-路由)
- [移动节点](#移动节点)

### 第四部分：使用指南
- [个人助理设置](#个人助理设置)
- [CLI 参考](#cli-参考)
- [CLI 自动化](#cli-自动化)

---

## 什么是 OpenClaw

**OpenClaw** 是一个**自托管网关**，将您最喜欢的聊天应用（WhatsApp、Telegram、Discord、iMessage 等）连接到 AI 编码 Agent（如 Pi）。

您在自己的机器（或服务器）上运行一个网关进程，它成为您的消息应用和始终可用的 AI 助理之间的桥梁。

### 适用人群

开发者和高级用户想要一个个人 AI 助理，他们可以从任何地方发送消息——无需放弃对数据的控制或依赖托管服务。

### OpenClaw 的不同之处

- **自托管**：运行在您的硬件上，您的规则
- **多渠道**：一个网关服务 WhatsApp、Telegram、Discord 等
- **Agent 原生**：为编码 Agent 构建，支持工具使用、会话、记忆和多 Agent 路由
- **开源**：MIT 许可，社区驱动

### 你需要什么

- **Node.js** — 推荐 Node 24（Node 22.16+ 也支持）
- **API Key** — 来自模型提供商（Anthropic、OpenAI、Google 等），onboarding 会提示您
- **5 分钟时间** — 快速安装和配置

检查 Node 版本：`node --version`

Windows 用户：原生 Windows 和 WSL2 都支持。WSL2 推荐用于生产使用。

---

## 工作原理

```
┌─────────────────┐
│  Chat apps      │
│  + plugins      │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│    Gateway      │
│  (OpenClaw)     │
└────────┬────────┘
         │
    ┌────────┬──────────┬──────────┐
    ↓         ↓          ↓          ↓
┌──────┐ ┌──────  ┌──────── ┌─────────┐
│Pi    │ │ CLI  │  │Web UI  │ │Mobile   │
│agent │ │      │  │        │ │nodes    │
└──────┘ └──────┘  └────────┘ └─────────
```

网关是所有会话、路由和渠道连接的**单一事实来源**。

---

## 关键功能

### 🚀 多渠道网关
WhatsApp、Telegram、Discord 和 iMessage 通过单个网关进程支持。

### 🔌 插件渠道
添加 Mattermost 和更多扩展包。

### 🔄 多 Agent 路由
每个 Agent、工作区或发送者的隔离会话。

### 📎 媒体支持
发送和接收图片、音频和文档。

### 🖥️ Web 控制 UI
用于聊天、配置、会话和节点的浏览器仪表板。

### 📱 移动节点
配对 iOS 和 Android 节点，用于 Canvas、相机和语音启用工作流。

---

## 快速开始

### 1. 安装 OpenClaw

```bash
npm install -g openclaw@latest
```

### 2. Onboarding 并安装服务

```bash
openclaw onboard --install-daemon
```

### 3. 聊天

在浏览器中打开 Control UI 并发送消息：

```bash
openclaw dashboard
```

或者连接一个渠道（**Telegram 最快**）并从手机聊天。

需要完整的安装和开发设置？请参阅 [Getting Started](#getting-started)。

---

## Dashboard 控制面板

网关启动后，在浏览器中打开 Control UI。

### 本地访问
- **默认地址**: `http://127.0.0.1:18789/`

### 远程访问
- **Web surfaces** 和 **Tailscale**

### Dashboard 功能
- 聊天界面
- 配置管理
- 会话查看
- 节点管理

---

## 配置说明

配置文件位于 `~/.openclaw/openclaw.json`

### 默认行为
- 如果**不配置任何内容**，OpenClaw 使用捆绑的 Pi 二进制文件，在 RPC 模式下运行，每发送者会话。

### 锁定配置
如果要锁定它，从 `channels.whatsapp.allowFrom` 开始，并为（群组）提及规则。

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
  }
}
```

---

## 安装 OpenClaw

### 系统要求

- **Node.js**: 24 推荐（22.16+ 支持）
- **操作系统**: 
  - Windows（原生或 WSL2）
  - macOS
  - Linux

### 安装步骤

1. **检查 Node 版本**
   ```bash
   node --version
   ```

2. **全局安装 OpenClaw**
   ```bash
   npm install -g openclaw@latest
   ```

3. **验证安装**
   ```bash
   openclaw --version
   ```

---

## Onboarding 引导

### CLI Onboarding

```bash
openclaw onboard
```

引导式设置，包括：
- API Key 配置
- 渠道连接
- 服务安装

### macOS App Onboarding

macOS 用户可以通过图形界面完成设置。

---

## 多渠道网关

### 支持的渠道

| 渠道 | 状态 | 设置难度 |
|------|------|---------|
| **Telegram** | ✅ 支持 | ⭐ 最简单 |
| **WhatsApp** | ✅ 支持 | ⭐⭐ 中等 |
| **Discord** | ✅ 支持 | ⭐⭐ 中等 |
| **iMessage** | ✅ 支持 | ⭐⭐⭐ 需要 macOS |
| **Mattermost** | 🔌 插件 | 需扩展包 |

### 渠道配置

每个渠道有独立的配置文件，位于 `~/.openclaw/channels/`

---

## Agent 路由

### 多 Agent 支持

OpenClaw 支持同时运行多个 AI Agent：

- **Pi Agent** - 默认编码 Agent
- **Claude** - 通过 API 集成
- **GPT** - 通过 API 集成
- **自定义 Agent** - 通过插件系统

### 会话隔离

- 每个 Agent 独立会话
- 工作区隔离
- 发送者隔离

---

## 移动节点

### iOS 节点

- 配对 iPhone
- Canvas 支持
- 相机集成
- 语音工作流

### Android 节点

- 配对 Android 设备
- 媒体共享
- 通知集成

---

## 个人助理设置

### 第一步：选择渠道

推荐从 **Telegram** 开始（设置最简单）

### 第二步：配置模型

选择您的 AI 模型提供商：
- Anthropic (Claude)
- OpenAI (GPT)
- Google (Gemini)

### 第三步：测试聊天

发送消息测试连接：
```
你好，请介绍一下自己
```

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

### 高级命令

```bash
# 安装为系统服务
openclaw onboard --install-daemon

# 重置配置
openclaw reset

# 导出配置
openclaw config export

# 导入配置
openclaw config import
```

---

## CLI 自动化

### 脚本示例

```bash
#!/bin/bash
# 自动启动 OpenClaw

openclaw start
sleep 5
openclaw dashboard
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

## 故障排查

### 常见问题

#### 1. 端口被占用

**错误**: `Port 18789 is already in use`

**解决**:
```bash
# 查找占用端口的进程
lsof -i :18789

# 杀掉进程
kill -9 <PID>

# 或者更改端口
openclaw config set port 18790
```

#### 2. API Key 无效

**错误**: `Invalid API key`

**解决**:
- 检查 API Key 是否正确复制
- 确认账户有可用额度
- 重新运行 onboarding: `openclaw onboard`

#### 3. 渠道连接失败

**错误**: `Failed to connect to channel`

**解决**:
- 检查网络连接
- 验证渠道凭证
- 查看日志：`openclaw logs`

---

## 安全最佳实践

### 1. API Key 保护

- 不要将 API Key 提交到 Git
- 使用环境变量或加密存储
- 定期轮换 Key

### 2. 访问控制

- 配置 `allowFrom` 限制允许的发送者
- 群组中要求 @提及
- 使用白名单 IP

### 3. 数据隐私

- 自托管确保数据控制
- 本地存储会话历史
- 不依赖第三方云服务

---

## 进阶配置

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

### 高级路由规则

```json
{
  "routing": {
    "rules": [
      {
        "pattern": ".*代码.*",
        "agent": "coding-agent",
        "priority": 1
      },
      {
        "pattern": ".*天气.*",
        "agent": "weather-agent",
        "priority": 2
      }
    ]
  }
}
```

---

## 资源链接

### 官方资源
- **官网**: https://openclaw.ai/
- **文档**: https://docs.openclaw.ai/
- **GitHub**: https://github.com/openclaw/openclaw
- **Discord**: https://discord.com/invite/clawd
- **Releases**: https://github.com/openclaw/openclaw/releases

### 社区资源
- **插件市场**: （即将推出）
- **用户论坛**: Discord 社区
- **问题反馈**: GitHub Issues

---

## 版本历史

### 最新版本
查看 GitHub Releases 获取最新版本信息。

### 更新日志
- 新增渠道支持
- 性能优化
- Bug 修复
- 安全更新

---

## 贡献指南

### 开发环境设置

```bash
# 克隆仓库
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 开发模式运行
npm run dev
```

### 提交代码

1. Fork 仓库
2. 创建分支：`git checkout -b feature/your-feature`
3. 提交更改：`git commit -am 'Add new feature'`
4. 推送分支：`git push origin feature/your-feature`
5. 创建 Pull Request

---

## 许可证

**MIT License**

Copyright (c) OpenClaw

允许免费使用、复制、修改、合并、出版、发行、再授权和/或销售本软件副本。

---

## 致谢

感谢所有贡献者和社区成员！

**"EXFOLIATE! EXFOLIATE!"** — A space lobster, probably

---

**文档版本**: 官方文档提取版 v1.0  
**最后更新**: 2026-03-22  
**内容来源**: https://docs.openclaw.ai/  
**提取方式**: 官方文档内容整理
