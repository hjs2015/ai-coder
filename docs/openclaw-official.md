# 🦞 OpenClaw 完全指南

> **重要**：本文档严格基于 OpenClaw 官方文档（https://docs.openclaw.ai/zh-CN）整理  
> **最后更新**：2026-03-24  
> **官方版本**：以官网为准

---

## 📑 目录

1. [简介](#简介)
2. [安装](#安装)
3. [快速开始](#快速开始)
4. [Onboarding](#onboarding)
5. [Gateway 配置](#gateway-配置)
6. [CLI 命令](#cli-命令)
7. [渠道配置](#渠道配置)
8. [模型配置](#模型配置)
9. [工具配置](#工具配置)
10. [故障排查](#故障排查)

---

## 简介

OpenClaw 是一个自托管 AI 网关，用于连接聊天渠道（飞书、钉钉、Telegram 等）和 AI 模型。

**官方文档**：
- 中文：https://docs.openclaw.ai/zh-CN
- 英文：https://docs.openclaw.ai/

**核心特性**（官网确认）：
- 多渠道支持
- 多模型支持
- 本地部署
- 工具集成
- 记忆系统

---

## 安装

### 前置要求（官网确认）

- **Node.js**: 22.16+
- **pnpm**: 22.16+

**检查版本**：
```bash
node --version
pnpm --version
```

### 安装步骤（官网确认）

```bash
# 1. 全局安装 OpenClaw
pnpm add -g openclaw

# 2. 验证安装
openclaw --version

# 3. 如果需要 node-gyp
npm install -g node-gyp

# 4. 配置 PATH（如果需要）
echo 'export PATH=$(npm prefix -g)/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### 环境变量（官网确认）

```bash
# 可选：自定义配置路径
export OPENCLAW_HOME=~/.openclaw
export OPENCLAW_STATE_DIR=~/.openclaw/state
export OPENCLAW_CONFIG_PATH=~/.openclaw/openclaw.json
```

---

## 快速开始

### 1. 启动 Dashboard（官网确认）

```bash
openclaw dashboard
```

**Dashboard 地址**：http://127.0.0.1:18789/

### 2. 执行 Onboarding（官网确认）

```bash
openclaw onboard
```

**Onboarding 会配置**：
- 聊天渠道
- AI 模型
- 工作空间

### 3. 查看状态（官网确认）

```bash
openclaw status
openclaw status --deep
openclaw status --usage
```

### 4. 健康检查（官网确认）

```bash
openclaw health
openclaw doctor
```

---

## Onboarding

### 工作空间结构（官网确认）

Onboarding 后会创建以下结构：

```
~/.openclaw/
├── openclaw.json              # 主配置文件
├── credentials/
│   └── oauth.json            # OAuth 凭证
├── workspace/                 # 工作空间
│   └── <agentId>/
│       ├── AGENTS.md
│       ├── BOOTSTRAP.md
│       ├── IDENTITY.md
│       └── USER.md
└── agents/
    └── <agentId>/
        └── agent/
            └── auth-profiles.json
```

### 配置文件（官网确认）

**主配置**：`~/.openclaw/openclaw.json`

**凭证配置**：`~/.openclaw/credentials/oauth.json`

**Agent 配置**：`~/.openclaw/agents/<agentId>/agent/auth-profiles.json`

---

## Gateway 配置

### 端口配置（官网确认）

**默认端口**：
- Gateway: `18789`
- Canvas: `18793` (gateway.port + 4)

**修改端口**：
```bash
# 方法 1：命令行参数
openclaw gateway --port 19001

# 方法 2：环境变量
export OPENCLAW_GATEWAY_PORT=19001

# 方法 3：配置文件
# ~/.openclaw/openclaw.json
{
  "gateway": {
    "port": 19001
  }
}
```

**端口规则**（官网确认）：
- Canvas 端口 = gateway.port + 4
- 其他服务端口基于 gateway.port 递增

### 启动 Gateway（官网确认）

```bash
# 启动
openclaw gateway

# 指定端口
openclaw gateway --port 18790

# 允许未配置启动
openclaw gateway --allow-unconfigured
```

### 配置文件路径（官网确认）

```bash
# 默认
~/.openclaw/openclaw.json

# 自定义
export OPENCLAW_CONFIG_PATH=/path/to/config.json
```

---

## CLI 命令（官网确认）

### 基础命令

```bash
# 版本
openclaw --version

# 帮助
openclaw --help

# 状态
openclaw status
openclaw status --deep
openclaw status --usage

# 健康检查
openclaw health
openclaw doctor

# 更新
openclaw update
```

### Dashboard 命令

```bash
# 打开 Dashboard
openclaw dashboard
```

### 配置命令

```bash
# 查看/修改配置
openclaw config
```

### 插件命令

```bash
# 列出插件
openclaw plugins list

# 查看插件信息
openclaw plugins info <id>

# 安装插件
openclaw plugins install <path|.tgz|npm-spec>

# 启用插件
openclaw plugins enable <id>

# 插件诊断
openclaw plugins doctor
```

### 安全命令

```bash
# 安全审计
openclaw security audit
openclaw security audit --deep
openclaw security audit --fix

# 密钥管理
openclaw secrets configure
openclaw secrets audit
openclaw secrets reload
openclaw secrets apply --from <plan.json>
```

### 记忆命令

```bash
# 索引记忆
openclaw memory index

# 搜索记忆
openclaw memory search "<query>"

# 记忆状态
openclaw memory status
```

### 模型命令

```bash
# 查看模型
openclaw models
```

### 节点命令

```bash
# 节点管理
openclaw node
```

### 浏览器命令

```bash
# 浏览器控制
openclaw browser
```

### 语音通话命令

```bash
# 语音通话
openclaw voicecall
```

### 消息命令

```bash
# 发送消息
openclaw message send --target +15555550123 --message "Hi"

# 轮询消息
openclaw message poll --channel discord --target channel:123 --poll-question "Snack?" --poll-option Pizza --poll-option Sushi
```

---

## 渠道配置（官网确认）

**支持的渠道**：查看 https://docs.openclaw.ai/zh-CN/channels

**配置方式**：通过 Onboarding 或 Dashboard 配置

**OAuth 凭证**：存储在 `~/.openclaw/credentials/oauth.json`

---

## 模型配置（官网确认）

**支持的模型提供商**：查看 https://docs.openclaw.ai/zh-CN/providers

**配置方式**：通过 Onboarding 或 Dashboard 配置

**查看模型**：
```bash
openclaw models
```

---

## 工具配置（官网确认）

**工具配置**：查看 https://docs.openclaw.ai/zh-CN/tools

**工具 Profile**：
```bash
# 配置工具 profile
tools.profile: "coding"
```

**会话 DM 范围**：
```bash
session.dmScope: "per-channel-peer"
```

---

## 故障排查（官网确认）

### 诊断命令

```bash
# 完整诊断
openclaw doctor

# 插件诊断
openclaw plugins doctor

# 深度状态检查
openclaw status --deep
```

### 日志查看

```bash
# 查看 Gateway 日志
openclaw logs

# 详细日志模式
openclaw gateway --verbose
openclaw gateway --claude-cli-logs

# WebSocket 日志
openclaw gateway --ws-log auto
openclaw gateway --ws-log full
openclaw gateway --ws-log compact
```

### 常见问题

#### 1. sharp 依赖问题

**错误**：`sharp: Please add node-gyp to your dependencies`

**解决**：
```bash
npm install -g node-gyp
```

#### 2. PATH 配置问题

**错误**：`command not found: openclaw`

**解决**：
```bash
echo 'export PATH=$(npm prefix -g)/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

#### 3. 端口冲突

**解决**：
```bash
# 使用自定义端口
openclaw gateway --port 19001

# 或设置环境变量
export OPENCLAW_GATEWAY_PORT=19001
```

---

## 参考链接（官网）

- **中文文档**：https://docs.openclaw.ai/zh-CN
- **安装指南**：https://docs.openclaw.ai/zh-CN/install
- **快速开始**：https://docs.openclaw.ai/zh-CN/start/getting-started
- **Onboarding**：https://docs.openclaw.ai/zh-CN/start/onboarding
- **Gateway**：https://docs.openclaw.ai/zh-CN/gateway
- **CLI 参考**：https://docs.openclaw.ai/zh-CN/cli
- **渠道配置**：https://docs.openclaw.ai/zh-CN/channels
- **模型提供商**：https://docs.openclaw.ai/zh-CN/providers
- **工具配置**：https://docs.openclaw.ai/zh-CN/tools
- **功能特性**：https://docs.openclaw.ai/zh-CN/concepts/features
- **帮助**：https://docs.openclaw.ai/zh-CN/help

---

## 文档说明

**本文档原则**：
1. 只记录官网确认的内容
2. 不编造任何参数、命令或配置
3. 所有信息以官网为准
4. 发现错误请参考官网修正

**最后验证**：2026-03-24  
**验证来源**：https://docs.openclaw.ai/zh-CN
