# 🦞 OpenClaw 完全指南（中国内地版）

> **自托管 AI 网关 · 本土化深度适配 · 保留官方核心架构**  
> **文档版本**: v6.0 完整版（2026-03-23）  
> **官方文档**: https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **许可证**: MIT  
> **适用地区**: 中国大陆及港澳台地区

---

## 📑 完整目录

<details>
<summary><b>点击展开完整目录（15 大部分 86 章节）</b></summary>

### 第一部分：产品认知与入门
1. [什么是 OpenClaw](#什么是-openclaw)
2. [核心价值与定位](#核心价值与定位)
3. [适用场景](#适用场景)
4. [快速开始（60 秒上手）](#快速开始 60-秒上手)
5. [系统要求与兼容性](#系统要求与兼容性)

### 第二部分：架构详解 ⭐
6. [整体架构图](#整体架构图)
7. [核心组件](#核心组件)
8. [消息流转流程](#消息流转流程)
9. [数据流与状态管理](#数据流与状态管理)

### 第三部分：CLI 命令参考 ⭐
10. [基础命令](#基础命令)
11. [Onboarding 命令](#onboarding-命令)
12. [Channel 命令](#channel-命令)
13. [Model 命令](#model-命令)
14. [Agent 命令](#agent-命令)
15. [Config 命令](#config-命令)
16. [Logs 与 Debug 命令](#logs-与-debug-命令)

### 第四部分：国内本土化适配专区 ⭐
17. [国内网络环境适配](#国内网络环境适配)
18. [国内大模型完整接入](#国内大模型完整接入)
19. [国内聊天平台接入](#国内聊天平台接入)
20. [国内镜像与加速方案](#国内镜像与加速方案)

### 第五部分：安装与部署
21. [npm 安装（推荐）](#npm-安装推荐)
22. [Docker 容器化部署](#docker-容器化部署)
23. [Docker Compose 部署](#docker-compose-部署)
24. [源码安装（开发者）](#源码安装开发者)
25. [离线安装方案](#离线安装方案)
26. [生产环境部署](#生产环境部署)

### 第六部分：国内聊天渠道配置 ⭐
27. [飞书配置（原生支持）](#飞书配置原生支持)
28. [企业微信配置](#企业微信配置)
29. [钉钉配置](#钉钉配置)
30. [微信配置（个人号/公众号）](#微信配置个人号公众号)
31. [QQ 配置](#qq-配置)
32. [Telegram 配置（备选）](#telegram-配置备选)

### 第七部分：国内大模型配置 ⭐
33. [通义千问（阿里云）](#通义千问阿里云)
34. [文心一言（百度）](#文心一言百度)
35. [豆包（火山引擎）](#豆包火山引擎)
36. [讯飞星火](#讯飞星火)
37. [Kimi（月之暗面）](#kimi-月之暗面)
38. [智谱 GLM](#智谱-glm)
39. [本地模型（Ollama）](#本地模型-ollama)

### 第八部分：渠道配置（国际）
40. [支持的渠道列表](#支持的渠道列表)
41. [WhatsApp 配置](#whatsapp-配置)
42. [Discord 配置](#discord-配置)
43. [iMessage 配置](#imessage-配置)
44. [渠道路由规则](#渠道路由规则)

### 第九部分：核心概念
45. [Gateway（网关）](#gateway-网关)
46. [Agent（智能体）](#agent-智能体)
47. [Session（会话）](#session-会话)
48. [Memory（记忆）](#memory-记忆)
49. [Workspace（工作区）](#workspace-工作区)

### 第十部分：Agent 与工具
50. [Agent 工作区配置](#agent-工作区配置)
51. [工具与插件系统](#工具与插件系统)
52. [MCP 协议集成](#mcp-协议集成)
53. [定时任务与自动化](#定时任务与自动化)

### 第十一部分：会话与记忆管理
54. [会话管理深度解析](#会话管理深度解析)
55. [记忆系统架构](#记忆系统架构)
56. [会话压缩机制](#会话压缩机制)

### 第十二部分：配置参考 ⭐
57. [配置文件结构](#配置文件结构)
58. [环境变量参考](#环境变量参考)
59. [配置项详解](#配置项详解)
60. [配置模板](#配置模板)

### 第十三部分：运维管理
61. [Gateway 运维管理](#gateway-运维管理)
62. [日志与调试](#日志与调试)
63. [监控与告警](#监控与告警)
64. [备份与恢复](#备份与恢复)
65. [升级与迁移](#升级与迁移)

### 第十四部分：安全与优化
66. [安全配置](#安全配置)
67. [性能优化](#性能优化)
68. [高可用配置](#高可用配置)

### 第十五部分：故障排查
69. [诊断命令速查](#诊断命令速查)
70. [网络问题排查](#网络问题排查)
71. [高频问题解决方案](#高频问题解决方案)
72. [FAQ（100+ 常见问题）](#faq100-常见问题)

### 附录
- [附录 A：完整 CLI 命令参考](#附录-a-完整-cli-命令参考)
- [附录 B：环境变量完整参考](#附录-b-环境变量完整参考)
- [附录 C：配置文件完整参考](#附录-c-配置文件完整参考)
- [附录 D：国内 API Key 获取指南](#附录-d-国内-api-key-获取指南)
- [附录 E：架构决策记录](#附录-e-架构决策记录)

</details>

---

## 第一部分：产品认知与入门

### 什么是 OpenClaw

**OpenClaw** 是一个**自托管 AI 网关**（Self-hosted AI Gateway），让你能够在自己的服务器上运行私人 AI 助手，并通过任意聊天平台进行交互。

#### 核心定义（中文解释）

| 术语 | 英文 | 中文解释 |
|------|------|---------|
| **自托管** | Self-hosted | 运行在你控制的服务器上，数据完全本地化 |
| **AI 网关** | AI Gateway | 统一管理多个 AI 模型的中间层 |
| **多渠道** | Multi-channel | 支持 30+ 聊天平台，一套配置连接所有平台 |
| **7×24 小时** | 24/7 | 持续运行，可执行定时任务、后台监控 |

#### 一句话总结

> OpenClaw = 你的私人 AI 助手 + 任意聊天平台 + 自托管控制 + 多模型支持

---

### 核心价值与定位

#### 与国内环境的适配价值

| 需求 | 传统方案 | OpenClaw 方案 |
|------|---------|--------------|
| **数据合规** | 数据出境风险 | ✅ 数据完全本地存储 |
| **网络依赖** | 需要访问外网 API | ✅ 支持国内大模型（阿里/百度/火山） |
| **聊天平台** | 仅支持国际平台 | ✅ 支持飞书/企微/钉钉/微信 |
| **成本** | 美元付费、汇率损失 | ✅ 人民币付费、国内 CDN |
| **响应速度** | 国际延迟高 | ✅ 国内节点、低延迟 |

#### 与国内同类产品的对比

| 产品 | OpenClaw | Coze/Dify | 萝卜塔 |
|------|----------|-----------|--------|
| **自托管** | ✅ 完全支持 | ⚠️ 部分支持 | ❌ SaaS |
| **多渠道** | 30+ | 有限 | 有限 |
| **模型中立** | ✅ 30+ 提供商 | ⚠️ 绑定平台 | ❌ 单一模型 |
| **数据控制** | ✅ 完全本地 | ⚠️ 云端存储 | ❌ 平台控制 |
| **成本** | 仅 API 费 | 订阅费 +API | 订阅费 |

---

### 适用场景

#### 国内用户专属场景

| 场景 | 使用平台 | 核心价值 |
|------|---------|---------|
| **飞书办公助手** | 飞书 | 工作群智能问答、会议纪要生成 |
| **企业微信客服** | 企业微信 | 自动回复客户咨询、工单处理 |
| **钉钉运维机器人** | 钉钉 | 服务器监控告警、自动部署 |
| **微信个人助理** | 微信 | 日程提醒、待办事项、知识管理 |
| **QQ 群管理** | QQ | 自动欢迎、违规检测、内容审核 |

#### 跨境场景

| 场景 | 使用平台 | 核心价值 |
|------|---------|---------|
| **外贸客服** | WhatsApp+ 微信 | 统一回复国内外客户 |
| **海外团队协作** | Slack+ 飞书 | 跨时区协作、文档翻译 |
| **跨境电商** | Telegram+ 微信 | 多平台订单管理、客服 |

---

### 快速开始（60 秒上手）

#### 前置要求

```bash
# 检查 Node.js 版本（需要 18+）
node --version
# 输出：v20.x.x

# 检查 npm
npm --version
# 输出：10.x.x
```

#### 三步安装（国内镜像加速）

```bash
# 1. 配置淘宝镜像（加速下载）
npm config set registry https://registry.npmmirror.com

# 2. 全局安装 OpenClaw
npm install -g openclaw

# 3. 启动 Onboarding（首次配置向导）
openclaw onboarding
```

#### 验证安装

```bash
# 查看状态
openclaw status

# 打开 Dashboard
openclaw dashboard
# 浏览器访问：http://localhost:3000
```

---

### 系统要求与兼容性

#### 国内系统兼容性

| 系统 | 版本要求 | 支持状态 | 备注 |
|------|---------|---------|------|
| **CentOS** | 7/8/9 | ✅ 完全支持 | 国内最常用 |
| **Ubuntu** | 20.04/22.04 | ✅ 完全支持 | 推荐 22.04 LTS |
| **Debian** | 10/11/12 | ✅ 完全支持 | 稳定可靠 |
| **OpenSUSE** | 15+ | ✅ 支持 | 企业常用 |
| **Windows** | 10/11 | ✅ 支持 | 原生或 WSL2 |
| **macOS** | 12.0+ | ✅ 支持 | Apple Silicon 优化 |

#### 硬件配置建议（国内场景）

| 配置 | 个人使用 | 小团队 | 企业生产 |
|------|---------|--------|---------|
| **CPU** | 2 核心 | 4 核心 | 8 核心 + |
| **内存** | 2GB | 4GB | 8GB+ |
| **存储** | 10GB SSD | 20GB SSD | 50GB+ SSD |
| **带宽** | 1Mbps | 5Mbps | 10Mbps+ |

---

## 第二部分：架构详解 ⭐

### 整体架构图

```
┌─────────────────────────────────────────────────────────────┐
│                      聊天平台层                              │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐          │
│  │  飞书   │ │企业微信 │ │  钉钉   │ │  微信   │  ...      │
│  └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘          │
└───────┼───────────┼───────────┼───────────┼────────────────┘
        │           │           │           │
        └───────────┴─────┬─────┴───────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                   OpenClaw Gateway                         │
│  ┌──────────────────────────────────────────────────────┐  │
│  │                 Channel Adapter                      │  │
│  │  统一消息格式转换（各平台→OpenClaw 标准格式）            │  │
│  └──────────────────────────────────────────────────────┘  │
│                          │                                  │
│  ┌───────────────────────▼───────────────────────────────┐ │
│  │                  Message Router                       │ │
│  │  根据规则路由到不同 Agent（关键词/用户/群组）            │  │
│  └───────────────────────┬───────────────────────────────┘ │
│                          │                                  │
│  ┌───────────────────────▼───────────────────────────────┐ │
│  │                    Agent Loop                         │ │
│  │  1. 接收消息 → 2. 加载上下文 → 3. 调用模型 → 4. 返回响应 │ │
│  └───────────────────────┬───────────────────────────────┘ │
│                          │                                  │
│  ┌───────────────────────▼───────────────────────────────┐ │
│  │                  Model Provider                       │ │
│  │  统一 API 接口（支持 30+ 模型提供商，自动故障转移）       │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────────────┐
│                      数据存储层                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │  SQLite/PG   │  │  本地文件    │  │  向量数据库  │      │
│  │  (会话历史)  │  │  (配置/日志) │  │  (记忆检索)  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

---

### 核心组件

#### 1. Gateway（网关）

**职责**：核心服务进程，管理所有 Channel、Agent 和 Model 连接

```bash
# 启动 Gateway
openclaw start

# 查看 Gateway 状态
openclaw status

# 停止 Gateway
openclaw stop

# 重启 Gateway
openclaw restart
```

**配置文件**：`~/.openclaw/openclaw.json`

```json
{
  "gateway": {
    "port": 3000,
    "host": "0.0.0.0",
    "logLevel": "info",
    "dataDir": "~/.openclaw/data"
  }
}
```

---

#### 2. Channel Adapter（渠道适配器）

**职责**：将各聊天平台的消息格式转换为 OpenClaw 标准格式

**支持的渠道**：

| 渠道 | 类型 | 状态 | 插件 |
|------|------|------|------|
| **飞书** | 企业 IM | ✅ 原生 | - |
| **企业微信** | 企业 IM | ✅ 社区 | @openclaw/channel-wecom |
| **钉钉** | 企业 IM | ✅ 社区 | @openclaw/channel-dingtalk |
| **微信** | 个人 IM | ⚠️ 社区 | @openclaw/channel-wechaty |
| **QQ** | 个人 IM | ⚠️ 社区 | @openclaw/channel-qq |
| **Telegram** | 国际 IM | ✅ 原生 | - |
| **Discord** | 社区 IM | ✅ 原生 | - |
| **WhatsApp** | 国际 IM | ⚠️ 社区 | @openclaw/channel-whatsapp |
| **Slack** | 企业 IM | ✅ 原生 | - |
| **iMessage** | 个人 IM | ⚠️ 实验 | @openclaw/channel-imessage |

**Channel 配置示例**：

```json
{
  "channels": {
    "feishu": {
      "appId": "cli_xxx",
      "appSecret": "xxx",
      "encryptKey": "xxx",
      "verificationToken": "xxx"
    },
    "telegram": {
      "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11"
    }
  }
}
```

---

#### 3. Message Router（消息路由器）

**职责**：根据规则将消息路由到不同的 Agent

**路由规则**：

```json
{
  "routing": {
    "defaultAgent": "default",
    "rules": [
      {
        "name": "coding-questions",
        "channel": "feishu",
        "pattern": ".*代码.*|.*编程.*|.*debug.*",
        "agent": "coding-agent",
        "priority": 10
      },
      {
        "name": "report-questions",
        "channel": "feishu",
        "pattern": ".*日报.*|.*周报.*|.*总结.*",
        "agent": "report-agent",
        "priority": 10
      },
      {
        "name": "user-specific",
        "channel": "feishu",
        "userId": "ou_xxxxxxxxxxxxx",
        "agent": "personal-agent",
        "priority": 20
      }
    ]
  }
}
```

**优先级说明**：
- 数字越大优先级越高
- 匹配多条规则时，使用优先级最高的
- 无匹配时使用 defaultAgent

---

#### 4. Agent Loop（智能体循环）

**职责**：处理消息的核心逻辑

**处理流程**：

```
1. 接收消息（从 Router）
   ↓
2. 加载会话上下文（从 Memory）
   ↓
3. 构建 Prompt（系统提示词 + 历史对话 + 当前消息）
   ↓
4. 调用模型（通过 Model Provider）
   ↓
5. 处理响应（文本/工具调用/错误处理）
   ↓
6. 保存会话（到 Memory）
   ↓
7. 返回响应（到 Channel）
```

**Agent 配置示例**：

```json
{
  "agents": {
    "default": {
      "model": "qwen-max",
      "systemPrompt": "你是一个有帮助的 AI 助手。",
      "temperature": 0.7,
      "maxTokens": 2048,
      "tools": ["search", "calculator"]
    },
    "coding-agent": {
      "model": "qwen-max",
      "systemPrompt": "你是一个专业的编程助手，擅长代码生成、调试和优化。",
      "temperature": 0.3,
      "maxTokens": 4096,
      "tools": ["code-interpreter", "file-reader"]
    }
  }
}
```

---

#### 5. Model Provider（模型提供商）

**职责**：统一管理多个 AI 模型提供商，支持故障转移和负载均衡

**支持的提供商**：

| 提供商 | 模型示例 | 状态 |
|--------|---------|------|
| **阿里云** | qwen-max, qwen-plus | ✅ |
| **百度** | ernie-4.0, ernie-3.5 | ✅ |
| **火山引擎** | doubao-pro, doubao-lite | ✅ |
| **讯飞** | spark-4.0, spark-3.5 | ✅ |
| **月之暗面** | moonshot-v1-8k, moonshot-v1-32k | ✅ |
| **智谱** | glm-4, glm-3-turbo | ✅ |
| **OpenAI** | gpt-4, gpt-3.5-turbo | ✅ |
| **Anthropic** | claude-3-opus, claude-3-sonnet | ✅ |
| **Google** | gemini-pro, gemini-ultra | ✅ |
| **Ollama** | llama2, qwen:7b | ✅ |

**Model 配置示例**：

```json
{
  "models": {
    "default": "qwen-max",
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxx",
        "baseUrl": "https://dashscope.aliyuncs.com/api/v1"
      },
      "qianfan": {
        "apiKey": "xxx",
        "secretKey": "xxx"
      },
      "openai": {
        "apiKey": "sk-xxx",
        "baseUrl": "https://api.openai.com/v1"
      }
    },
    "fallbacks": [
      {
        "from": "qwen-max",
        "to": ["qwen-plus", "ernie-4.0"]
      }
    ]
  }
}
```

---

### 消息流转流程

#### 完整消息流示例

```
用户（飞书）: "@OpenClaw 帮我写一个 Python 脚本，计算斐波那契数列"
   ↓
1. 飞书 API 推送消息到 OpenClaw Webhook
   ↓
2. Channel Adapter 转换消息格式
   {
     "channel": "feishu",
     "userId": "ou_xxx",
     "groupId": "oc_xxx",
     "content": "帮我写一个 Python 脚本，计算斐波那契数列",
     "timestamp": 1711180800
   }
   ↓
3. Message Router 匹配规则
   匹配到 "coding-questions" 规则 → 路由到 coding-agent
   ↓
4. Agent Loop 处理
   - 加载会话历史（最近 10 条对话）
   - 构建 Prompt：
     System: "你是一个专业的编程助手..."
     History: [用户：..., AI: ...]
     Current: "帮我写一个 Python 脚本..."
   ↓
5. Model Provider 调用模型
   - 选择模型：qwen-max
   - 发送请求到阿里云 DashScope API
   - 接收响应
   ↓
6. 处理响应
   - 提取文本内容
   - 保存会话到 SQLite
   ↓
7. 返回响应到飞书
   "@用户 好的，这是一个计算斐波那契数列的 Python 脚本：..."
```

---

### 数据流与状态管理

#### 数据存储结构

```
~/.openclaw/
├── openclaw.json          # 主配置文件
├── data/
│   ├── sessions.db        # SQLite 会话数据库
│   ├── memory/            # 向量记忆存储
│   │   ├── collections/   # 记忆集合
│   │   └── embeddings/    # 向量嵌入缓存
│   └── logs/              # 日志文件
│       ├── gateway.log
│       ├── channels.log
│       └── agents.log
└── agents/                # Agent 工作区
    ├── default/
    │   ├── workspace/     # 工作区文件
    │   └── config.json    # Agent 配置
    └── coding-agent/
        ├── workspace/
        └── config.json
```

#### 会话数据结构

```json
{
  "sessionId": "feishu:ou_xxx:oc_xxx:1711180800",
  "channel": "feishu",
  "userId": "ou_xxx",
  "groupId": "oc_xxx",
  "agent": "coding-agent",
  "messages": [
    {
      "role": "user",
      "content": "帮我写一个 Python 脚本",
      "timestamp": 1711180800
    },
    {
      "role": "assistant",
      "content": "好的，这是一个...",
      "timestamp": 1711180805
    }
  ],
  "metadata": {
    "model": "qwen-max",
    "tokens": 1234,
    "cost": 0.05
  }
}
```

---

## 第三部分：CLI 命令参考 ⭐

### 基础命令

#### openclaw --version

查看 OpenClaw 版本

```bash
openclaw --version
# 输出：openclaw/2026.3.12 linux-x64 node-v20.11.0
```

---

#### openclaw --help

查看所有可用命令

```bash
openclaw --help
# 输出：
# OpenClaw CLI - Self-hosted AI Gateway
#
# USAGE
#   openclaw <command> [options]
#
# COMMANDS
#   start          启动 Gateway 服务
#   stop           停止 Gateway 服务
#   restart        重启 Gateway 服务
#   status         查看服务状态
#   onboarding     首次配置向导
#   channel        渠道管理
#   model          模型管理
#   agent          Agent 管理
#   config         配置管理
#   logs           查看日志
#   dashboard      打开 Dashboard
#   doctor         诊断工具
#   --version      查看版本
#   --help         查看帮助
```

---

#### openclaw start

启动 Gateway 服务

```bash
# 前台启动（开发调试）
openclaw start

# 后台启动（生产环境）
openclaw start --daemon

# 指定配置文件
openclaw start --config /path/to/openclaw.json

# 指定日志级别
openclaw start --log-level debug
```

**选项**：
- `--daemon, -d`: 后台运行
- `--config, -c`: 指定配置文件路径
- `--log-level, -l`: 日志级别（debug/info/warn/error）
- `--port, -p`: 覆盖默认端口

---

#### openclaw stop

停止 Gateway 服务

```bash
# 优雅停止（等待当前请求完成）
openclaw stop

# 强制停止（立即终止）
openclaw stop --force
```

**选项**：
- `--force, -f`: 强制停止

---

#### openclaw restart

重启 Gateway 服务

```bash
openclaw restart

# 重启并更改日志级别
openclaw restart --log-level debug
```

---

#### openclaw status

查看服务状态

```bash
openclaw status
# 输出：
# OpenClaw Gateway Status
# ├─ Status: running
# ├─ PID: 12345
# ├─ Port: 3000
# ├─ Uptime: 2d 5h 30m
# ├─ Memory: 256MB
# ├─ Channels: 2 active (feishu, telegram)
# └─ Agents: 3 loaded (default, coding-agent, report-agent)
```

---

### Onboarding 命令

#### openclaw onboarding

首次配置向导

```bash
openclaw onboarding
# 交互式配置流程：
# 1. 选择聊天渠道（飞书/Telegram/...）
# 2. 输入渠道凭证
# 3. 选择默认模型
# 4. 输入模型 API Key
# 5. 测试连接
# 6. 保存配置
```

**交互式流程示例**：

```
🦞 OpenClaw Onboarding Wizard

Step 1/5: Choose your first channel
  ○ Telegram
  ● Feishu (推荐)
  ○ WeCom
  ○ DingTalk
  ○ Skip for now

Step 2/5: Feishu Configuration
  App ID: cli_xxxxxxxxxxxxx
  App Secret: [hidden]
  Encrypt Key: [hidden]
  Verification Token: [hidden]

Step 3/5: Choose default model
  ○ Qwen-Max (阿里云)
  ● ERNIE-4.0 (百度)
  ○ Doubao-Pro (火山引擎)
  ○ GPT-4 (OpenAI)

Step 4/5: API Key
  Enter your API Key: sk-xxxxxxxxxxxxxxxxx

Step 5/5: Test Connection
  ✓ Channel connected
  ✓ Model API working
  ✓ Configuration saved

🎉 Setup complete! Run 'openclaw start' to begin.
```

---

### Channel 命令

#### openclaw channel list

列出所有已配置的渠道

```bash
openclaw channel list
# 输出：
# Configured Channels
# ├─ feishu (active)
# │  ├─ App ID: cli_xxx
# │  └─ Status: connected
# ├─ telegram (active)
# │  ├─ Bot: @MyBot
# │  └─ Status: connected
# └─ wecom (inactive)
#    └─ Status: not configured
```

---

#### openclaw channel add

添加新渠道

```bash
# 交互式添加
openclaw channel add

# 指定渠道类型
openclaw channel add telegram

# 从配置文件导入
openclaw channel add --from-file channel-config.json
```

---

#### openclaw channel remove

删除渠道

```bash
openclaw channel remove feishu

# 强制删除（跳过确认）
openclaw channel remove feishu --force
```

---

#### openclaw channel test

测试渠道连接

```bash
openclaw channel test feishu
# 输出：
# Testing Feishu channel...
# ✓ API credentials valid
# ✓ Webhook reachable
# ✓ Bot can send messages
# ✓ Bot can receive messages
# Channel test passed!
```

---

### Model 命令

#### openclaw model list

列出所有已配置的模型

```bash
openclaw model list
# 输出：
# Configured Models
# ├─ qwen-max (default)
# │  ├─ Provider: DashScope
# │  ├─ Status: active
# │  └─ Cost: ¥0.04/1K tokens
# ├─ ernie-4.0
# │  ├─ Provider: Qianfan
# │  ├─ Status: active
# │  └─ Cost: ¥0.03/1K tokens
# └─ doubao-pro
#    ├─ Provider: Volcengine
#    └─ Status: inactive
```

---

#### openclaw model add

添加新模型

```bash
# 交互式添加
openclaw model add

# 指定提供商
openclaw model add dashscope

# 快速添加
openclaw model add dashscope --api-key sk-xxx --model qwen-max
```

---

#### openclaw model test

测试模型 API

```bash
openclaw model test qwen-max
# 输出：
# Testing qwen-max model...
# ✓ API key valid
# ✓ Request sent (50 tokens)
# ✓ Response received (120 tokens)
# ✓ Latency: 1.2s
# Model test passed!
```

---

#### openclaw model set-default

设置默认模型

```bash
openclaw model set-default qwen-max
# 输出：Default model set to qwen-max
```

---

### Agent 命令

#### openclaw agent list

列出所有 Agent

```bash
openclaw agent list
# 输出：
# Loaded Agents
# ├─ default
# │  ├─ Model: qwen-max
# │  ├─ System: "你是一个有帮助的 AI 助手"
# │  └─ Tools: search, calculator
# ├─ coding-agent
# │  ├─ Model: qwen-max
# │  ├─ System: "你是一个专业的编程助手"
# │  └─ Tools: code-interpreter, file-reader
# └─ report-agent
#    ├─ Model: ernie-4.0
#    ├─ System: "你是一个专业的报告生成助手"
#    └─ Tools: none
```

---

#### openclaw agent create

创建新 Agent

```bash
# 交互式创建
openclaw agent create

# 快速创建
openclaw agent create coding-agent \
  --model qwen-max \
  --system-prompt "你是一个专业的编程助手" \
  --tools code-interpreter,file-reader
```

---

#### openclaw agent edit

编辑 Agent 配置

```bash
openclaw agent edit coding-agent
# 打开编辑器修改配置
```

---

#### openclaw agent remove

删除 Agent

```bash
openclaw agent remove coding-agent

# 强制删除
openclaw agent remove coding-agent --force
```

---

### Config 命令

#### openclaw config view

查看当前配置

```bash
openclaw config view
# 输出完整配置（隐藏敏感信息）
```

---

#### openclaw config edit

编辑配置文件

```bash
openclaw config edit
# 打开默认编辑器（vim/nano）
```

---

#### openclaw config validate

验证配置文件

```bash
openclaw config validate
# 输出：
# ✓ Configuration file is valid
# ✓ All channels configured correctly
# ✓ All models have valid API keys
# ✓ All agents reference existing models
```

---

#### openclaw config export

导出配置

```bash
# 导出完整配置（不含密钥）
openclaw config export

# 导出完整配置（含密钥，注意保密）
openclaw config export --include-secrets

# 导出到文件
openclaw config export --output backup.json
```

---

#### openclaw config import

导入配置

```bash
openclaw config import backup.json

# 强制导入（覆盖现有配置）
openclaw config import backup.json --force
```

---

### Logs 与 Debug 命令

#### openclaw logs

查看日志

```bash
# 实时查看日志
openclaw logs

# 查看最近 100 行
openclaw logs --lines 100

# 仅查看错误
openclaw logs --level error

# 仅查看特定渠道
openclaw logs --channel feishu

# 导出日志
openclaw logs --output logs.txt
```

**选项**：
- `--lines, -n`: 显示行数（默认 100）
- `--level, -l`: 日志级别（debug/info/warn/error）
- `--channel, -c`: 过滤渠道
- `--output, -o`: 导出到文件
- `--follow, -f`: 实时跟踪（默认）

---

#### openclaw doctor

诊断工具

```bash
openclaw doctor
# 输出：
# OpenClaw Doctor
#
# System
# ✓ Node.js v20.11.0
# ✓ npm 10.2.4
# ✓ OS: Linux 5.15.0
#
# Configuration
# ✓ Config file exists
# ✓ Config is valid JSON
# ✓ All required fields present
#
# Channels
# ✓ Feishu: connected
# ✓ Telegram: connected
#
# Models
# ✓ qwen-max: API working
# ✓ ernie-4.0: API working
#
# Network
# ✓ DashScope API reachable (200ms)
# ✓ Qianfan API reachable (150ms)
#
# All checks passed!
```

---

#### openclaw debug

调试模式

```bash
# 启用调试模式
openclaw debug enable

# 禁用调试模式
openclaw debug disable

# 查看调试状态
openclaw debug status
```

---

#### openclaw dashboard

打开 Dashboard

```bash
openclaw dashboard
# 输出：
# Opening dashboard at http://localhost:3000
# (自动打开默认浏览器)
```

**Dashboard 功能**：
- 实时监控消息流
- 查看会话历史
- 管理 Agent 配置
- 查看 Token 使用统计
- 查看成本分析

---

## 第四部分：国内本土化适配专区 ⭐
### 国内网络环境适配

#### 问题背景

由于网络环境限制，中国大陆用户访问国际 AI 服务可能遇到：
- API 连接超时
- DNS 解析失败
- HTTPS 证书验证错误
- 响应速度慢

#### 解决方案

**方案 1：代理配置（推荐）**

```bash
# 系统级代理
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890

# OpenClaw 配置
export OPENCLAW_PROXY_URL=http://127.0.0.1:7890
```

**方案 2：直连国内服务**

- 使用国内大模型（通义/文心/豆包等）
- 使用国内聊天平台（飞书/企微/钉钉）
- 无需代理，稳定快速

**方案 3：混合模式**

- 国内服务直连
- 国际服务代理
- 自动路由选择

---

### 国内大模型完整接入

#### 支持的国内大模型

| 厂商 | 模型 | 上下文 | 价格 |
|------|------|--------|------|
| 阿里云 | 通义千问 | 32k | ¥0.02/1k tokens |
| 百度 | 文心一言 | 128k | ¥0.012/1k tokens |
| 火山引擎 | 豆包 | 128k | ¥0.0008/1k tokens |
| 讯飞 | 星火 | 128k | ¥0.003/1k tokens |
| 月之暗面 | Kimi | 200k | ¥0.004/1k tokens |
| 智谱 AI | GLM-4 | 128k | ¥0.08/1k tokens |

#### 配置示例

**通义千问**：
```yaml
models:
  - name: qwen-max
    provider: dashscope
    api_key: ${DASHSCOPE_API_KEY}
    model: qwen-max
```

**文心一言**：
```yaml
models:
  - name: ernie-bot-4
    provider: qianfan
    api_key: ${QIANFAN_AK}
    secret_key: ${QIANFAN_SK}
    model: ernie-bot-4
```

**豆包**：
```yaml
models:
  - name: doubao-pro-32k
    provider: volcengine
    access_key: ${VOLCENGINE_ACCESS_KEY}
    secret_key: ${VOLCENGINE_SECRET_KEY}
    model: doubao-pro-32k
```

---

### 国内聊天平台接入

#### 支持的平台

| 平台 | 支持类型 | 配置难度 |
|------|----------|----------|
| 飞书 | 机器人 | ⭐⭐ |
| 企业微信 | 机器人 | ⭐⭐ |
| 钉钉 | 机器人 | ⭐⭐ |
| 微信 | 个人号/公众号 | ⭐⭐⭐⭐ |
| QQ | 机器人 | ⭐⭐⭐ |

#### 飞书配置步骤

1. 创建飞书应用
2. 获取 App ID 和 App Secret
3. 配置事件订阅
4. 添加机器人到群聊

#### 企业微信配置

1. 创建企业微信应用
2. 获取 CorpID 和 Secret
3. 配置可信域名
4. 启用 API 接收消息

#### 钉钉配置

1. 创建钉钉机器人应用
2. 获取 AppKey 和 AppSecret
3. 配置消息接收地址
4. 安装到企业

---

### 国内镜像与加速方案

#### npm 镜像

```bash
# 使用淘宝镜像
npm config set registry https://registry.npmmirror.com

# 或使用腾讯云镜像
npm config set registry https://mirrors.cloud.tencent.com/npm/
```

#### Docker 镜像

```json
// /etc/docker/daemon.json
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://registry.docker-cn.com"
  ]
}
```

#### GitHub 加速

```bash
# 使用代理
git -c http.proxy=http://127.0.0.1:7890 clone https://github.com/openclaw/openclaw.git

# 或使用 Gitee 镜像
git clone https://gitee.com/mirror/openclaw.git
```

#### PyPI 镜像

```bash
# 使用清华镜像
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 或使用阿里云镜像
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
```

---
---

## 附录 A：完整 CLI 命令参考

### 命令速查表

| 命令 | 功能 | 示例 |
|------|------|------|
| `openclaw start` | 启动服务 | `openclaw start --daemon` |
| `openclaw stop` | 停止服务 | `openclaw stop --force` |
| `openclaw restart` | 重启服务 | `openclaw restart` |
| `openclaw status` | 查看状态 | `openclaw status` |
| `openclaw onboarding` | 配置向导 | `openclaw onboarding` |
| `openclaw channel list` | 列出渠道 | `openclaw channel list` |
| `openclaw channel add` | 添加渠道 | `openclaw channel add telegram` |
| `openclaw channel test` | 测试渠道 | `openclaw channel test feishu` |
| `openclaw model list` | 列出模型 | `openclaw model list` |
| `openclaw model test` | 测试模型 | `openclaw model test qwen-max` |
| `openclaw agent list` | 列出 Agent | `openclaw agent list` |
| `openclaw config view` | 查看配置 | `openclaw config view` |
| `openclaw logs` | 查看日志 | `openclaw logs --level error` |
| `openclaw doctor` | 诊断工具 | `openclaw doctor` |
| `openclaw dashboard` | 打开面板 | `openclaw dashboard` |

---

## 附录 B：环境变量完整参考

### 核心环境变量

| 变量名 | 说明 | 默认值 | 示例 |
|--------|------|--------|------|
| `OPENCLAW_PORT` | Gateway 端口 | 3000 | 3000 |
| `OPENCLAW_HOST` | 监听地址 | 0.0.0.0 | 127.0.0.1 |
| `OPENCLAW_LOG_LEVEL` | 日志级别 | info | debug |
| `OPENCLAW_DATA_DIR` | 数据目录 | ~/.openclaw/data | /var/lib/openclaw |
| `OPENCLAW_CONFIG_FILE` | 配置文件路径 | ~/.openclaw/openclaw.json | /etc/openclaw/config.json |

### 模型 API Key

| 变量名 | 提供商 | 获取方式 |
|--------|--------|---------|
| `DASHSCOPE_API_KEY` | 阿里云通义千问 | https://dashscope.console.aliyun.com/apiKey |
| `QIANFAN_API_KEY` | 百度文心一言 | https://console.bce.baidu.com/qianfan/ais/console/applicationConsole/application |
| `QIANFAN_SECRET_KEY` | 百度文心一言 | 同上 |
| `VOLCENGINE_ACCESS_KEY` | 火山引擎豆包 | https://console.volcengine.com/iam/keymanage/ |
| `VOLCENGINE_SECRET_KEY` | 火山引擎豆包 | 同上 |
| `OPENAI_API_KEY` | OpenAI | https://platform.openai.com/api-keys |
| `ANTHROPIC_API_KEY` | Anthropic | https://console.anthropic.com/settings/keys |

---

## 附录 C：配置文件完整参考

### 完整配置示例

```json
{
  "gateway": {
    "port": 3000,
    "host": "0.0.0.0",
    "logLevel": "info",
    "dataDir": "~/.openclaw/data"
  },
  "channels": {
    "feishu": {
      "appId": "cli_xxx",
      "appSecret": "xxx",
      "encryptKey": "xxx",
      "verificationToken": "xxx",
      "allowUsers": [],
      "allowGroups": [],
      "requireMention": true
    },
    "telegram": {
      "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11",
      "allowUsers": [],
      "allowGroups": []
    }
  },
  "models": {
    "default": "qwen-max",
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxx",
        "baseUrl": "https://dashscope.aliyuncs.com/api/v1"
      },
      "qianfan": {
        "apiKey": "xxx",
        "secretKey": "xxx"
      }
    },
    "fallbacks": [
      {
        "from": "qwen-max",
        "to": ["qwen-plus", "ernie-4.0"]
      }
    ]
  },
  "agents": {
    "default": {
      "model": "qwen-max",
      "systemPrompt": "你是一个有帮助的 AI 助手。",
      "temperature": 0.7,
      "maxTokens": 2048,
      "tools": []
    },
    "coding-agent": {
      "model": "qwen-max",
      "systemPrompt": "你是一个专业的编程助手。",
      "temperature": 0.3,
      "maxTokens": 4096,
      "tools": ["code-interpreter"]
    }
  },
  "routing": {
    "defaultAgent": "default",
    "rules": [
      {
        "name": "coding",
        "pattern": ".*代码.*|.*编程.*",
        "agent": "coding-agent",
        "priority": 10
      }
    ]
  },
  "memory": {
    "enabled": true,
    "maxSessions": 100,
    "maxMessagesPerSession": 50,
    "vectorStore": {
      "provider": "local",
      "dimensions": 768
    }
  }
}
```

---

## 第五部分：安装与部署

---

## 高级部署 ⭐⭐

### Docker 容器化部署

#### Dockerfile

```dockerfile
FROM node:20-alpine
RUN apk add --no-cache git python3 make g++
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 8088
CMD ["npm", "start"]
```

#### docker-compose.yml

```yaml
version: '3.8'
services:
  openclaw:
    build: .
    container_name: openclaw
    restart: unless-stopped
    ports:
      - "8088:8088"
    volumes:
      - ./config:/app/config
      - ./data:/data/openclaw
    environment:
      - NODE_ENV=production
      - TELEGRAM_BOT_TOKEN=${TELEGRAM_BOT_TOKEN}
      - OPENAI_API_KEY=${OPENAI_API_KEY}
```

#### 部署命令

```bash
docker-compose build
docker-compose up -d
docker-compose logs -f
```

---

### 多实例部署

#### Nginx 负载均衡

```nginx
upstream openclaw_backend {
    least_conn;
    server 127.0.0.1:8081;
    server 127.0.0.1:8082;
    server 127.0.0.1:8083;
}

server {
    listen 80;
    location / {
        proxy_pass http://openclaw_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

#### 启动多实例

```bash
OPENCLAW_PORT=8081 OPENCLAW_INSTANCE_ID=1 openclaw start --daemon
OPENCLAW_PORT=8082 OPENCLAW_INSTANCE_ID=2 openclaw start --daemon
OPENCLAW_PORT=8083 OPENCLAW_INSTANCE_ID=3 openclaw start --daemon
```

---

### 远程网关部署

```bash
ssh user@vps.example.com
curl -fsSL https://openclaw.ai/install.sh | bash
sudo systemctl enable openclaw && sudo systemctl start openclaw
sudo ufw allow 8088/tcp
openclaw connect --host vps.example.com --port 8088
```

---

### Tailscale 安全暴露

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up --authkey=tskey-auth-xxx
tailscale ip
openclaw config set gateway.host=$(tailscale ip)
openclaw connect --host 100.x.y.z --port 8088
```

---


### npm 安装（推荐）

#### 前置要求

```bash
# 检查 Node.js 版本（需要 18+）
node --version
# 输出：v20.x.x

# 检查 npm
npm --version
# 输出：10.x.x
```

#### 安装步骤

```bash
# 1. 配置淘宝镜像（加速下载）
npm config set registry https://registry.npmmirror.com

# 2. 全局安装 OpenClaw
npm install -g openclaw

# 3. 验证安装
openclaw --version
# 输出：openclaw/2026.3.12 linux-x64 node-v20.11.0
```

#### 升级

```bash
# 升级到最新版本
npm update -g openclaw

# 指定版本
npm install -g openclaw@2026.3.12
```

---

### Docker 容器化部署

#### 前置要求

```bash
# 检查 Docker 版本
docker --version
# 输出：Docker version 24.x.x

# 检查 Docker Compose
docker compose version
# 输出：Docker Compose version v2.x.x
```

#### 快速启动

```bash
# 1. 创建配置目录
mkdir -p ~/.openclaw
cd ~/.openclaw

# 2. 下载配置文件模板
curl -O https://raw.githubusercontent.com/openclaw/openclaw/main/examples/openclaw.json

# 3. 编辑配置文件
vim openclaw.json

# 4. 启动容器
docker run -d \
  --name openclaw \
  -p 3000:3000 \
  -v ~/.openclaw:/root/.openclaw \
  -e DASHSCOPE_API_KEY=sk-xxx \
  openclaw/openclaw:latest
```

#### 查看日志

```bash
# 实时日志
docker logs -f openclaw

# 最近 100 行
docker logs --tail 100 openclaw
```

#### 停止和删除

```bash
# 停止
docker stop openclaw

# 删除
docker rm openclaw
```

---

### Docker Compose 部署

#### 创建 docker-compose.yml

```yaml
version: '3.8'

services:
  openclaw:
    image: openclaw/openclaw:latest
    container_name: openclaw
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - ./config:/root/.openclaw
      - ./data:/root/.openclaw/data
      - ./logs:/var/log/openclaw
    environment:
      - OPENCLAW_LOG_LEVEL=info
      - DASHSCOPE_API_KEY=sk-xxx
      - QIANFAN_API_KEY=xxx
      - QIANFAN_SECRET_KEY=xxx
    networks:
      - openclaw-net

networks:
  openclaw-net:
    driver: bridge
```

#### 启动服务

```bash
# 后台启动
docker compose up -d

# 查看状态
docker compose ps

# 查看日志
docker compose logs -f
```

#### 停止服务

```bash
# 停止
docker compose down

# 停止并删除数据卷
docker compose down -v
```

---

### 源码安装（开发者）

#### 克隆仓库

```bash
# 使用 GitHub
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 或使用 Gitee 镜像（国内加速）
git clone https://gitee.com/openclaw/openclaw.git
cd openclaw
```

#### 安装依赖

```bash
# 配置淘宝镜像
npm config set registry https://registry.npmmirror.com

# 安装依赖
npm install

# 开发模式安装（包含 devDependencies）
npm install --also=dev
```

#### 构建

```bash
# 构建生产版本
npm run build

# 开发模式（热重载）
npm run dev
```

#### 运行

```bash
# 开发模式
npm run start:dev

# 生产模式
npm run start:prod

# 测试模式
npm run test
```

---

### 离线安装方案

#### 场景说明

适用于：
- 内网服务器（无外网访问）
- 高安全环境（网络隔离）
- 网络不稳定地区

#### 步骤

```bash
# 1. 在有网络的机器上下载
npm pack openclaw
# 输出：openclaw-2026.3.12.tgz

# 2. 下载依赖包
npm install --pack openclaw

# 3. 复制到离线机器
scp openclaw-*.tgz user@offline-server:/tmp/

# 4. 离线安装
npm install -g /tmp/openclaw-2026.3.12.tgz
```

#### 完整离线包

```bash
# 创建完整离线包（包含所有依赖）
npm pack --offline

# 解压
tar -xzf openclaw-2026.3.12.tgz

# 查看内容
ls package/
```

---

### 生产环境部署

#### 系统服务配置（systemd）

```bash
# 创建服务文件
sudo vim /etc/systemd/system/openclaw.service
```

**服务文件内容**：

```ini
[Unit]
Description=OpenClaw Gateway
After=network.target

[Service]
Type=simple
User=openclaw
Group=openclaw
WorkingDirectory=/opt/openclaw
ExecStart=/usr/bin/openclaw start --daemon
Restart=on-failure
RestartSec=10
Environment="OPENCLAW_LOG_LEVEL=info"
Environment="DASHSCOPE_API_KEY=sk-xxx"

# 安全加固
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ProtectHome=true

[Install]
WantedBy=multi-user.target
```

#### 启用服务

```bash
# 重载 systemd
sudo systemctl daemon-reload

# 启用服务
sudo systemctl enable openclaw

# 启动服务
sudo systemctl start openclaw

# 查看状态
sudo systemctl status openclaw
```

#### 日志管理

```bash
# 查看日志
sudo journalctl -u openclaw -f

# 最近 100 行
sudo journalctl -u openclaw -n 100

# 按时间过滤
sudo journalctl -u openclaw --since "2026-03-23 00:00:00"
```

---

## 第六部分：国内聊天渠道配置 ⭐

### 飞书配置（原生支持）

#### 前置准备

1. 登录 [飞书开放平台](https://open.feishu.cn/)
2. 创建企业应用
3. 获取 App ID 和 App Secret

#### 配置步骤

```bash
# 1. 编辑配置文件
openclaw config edit

# 2. 添加飞书渠道配置
{
  "channels": {
    "feishu": {
      "appId": "cli_xxxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxx",
      "encryptKey": "xxxxxxxxxxxxxxxxx",
      "verificationToken": "xxxxxxxxxxxxxxxxx",
      "requireMention": true,
      "allowUsers": [],
      "allowGroups": []
    }
  }
}

# 3. 验证配置
openclaw config validate

# 4. 重启服务
openclaw restart
```

#### 飞书开放平台配置

1. **事件订阅**
   - 订阅地址：`https://your-domain.com/api/channels/feishu/webhook`
   - 验证 Token：填写配置文件中的 `verificationToken`
   - 加密 Key：填写配置文件中的 `encryptKey`

2. **订阅事件**
   - `im.message.receive_v1` - 接收消息
   - `im.message.read_v1` - 消息已读（可选）

3. **权限配置**
   - 机器人发送消息
   - 获取用户信息
   - 加入群聊

#### 测试

```bash
# 测试飞书渠道
openclaw channel test feishu
```

---

### 企业微信配置

#### 安装插件

```bash
npm install -g @openclaw/channel-wecom
```

#### 配置步骤

1. 登录 [企业微信管理后台](https://work.weixin.qq.com/)
2. 创建自建应用
3. 获取 Agent ID 和 Secret

```json
{
  "channels": {
    "wecom": {
      "corpId": "wwxxxxxxxxxxxx",
      "agentId": 1000001,
      "secret": "xxxxxxxxxxxxxxxxx",
      "token": "xxxxxxxxxxxxxxxxx",
      "encodingAesKey": "xxxxxxxxxxxxxxxxx"
    }
  }
}
```

---

### 钉钉配置

#### 安装插件

```bash
npm install -g @openclaw/channel-dingtalk
```

#### 配置步骤

1. 登录 [钉钉开放平台](https://open-dev.dingtalk.com/)
2. 创建机器人应用
3. 获取 AppKey 和 AppSecret

```json
{
  "channels": {
    "dingtalk": {
      "appKey": "xxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxx",
      "encryptKey": "xxxxxxxxxxxxxxxxx",
      "verificationToken": "xxxxxxxxxxxxxxxxx"
    }
  }
}
```

---

### 微信配置（个人号/公众号）

#### 安装插件

```bash
npm install -g @openclaw/channel-wechaty
```

#### 个人号配置（Wechaty）

```json
{
  "channels": {
    "wechat": {
      "provider": "wechaty",
      "puppet": "wechaty-puppet-wechat4u",
      "head": true
    }
  }
}
```

#### 公众号配置

```json
{
  "channels": {
    "wechat-official": {
      "appId": "xxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxx",
      "token": "xxxxxxxxxxxxxxxxx",
      "encodingAesKey": "xxxxxxxxxxxxxxxxx"
    }
  }
}
```

---

### QQ 配置

#### 安装插件

```bash
npm install -g @openclaw/channel-qq
```

#### 配置（OneBot 协议）

```json
{
  "channels": {
    "qq": {
      "protocol": "onebot",
      "wsUrl": "ws://127.0.0.1:8080",
      "accessToken": "xxxxxxxxxxxxxxxxx"
    }
  }
}
```

---

### Telegram 配置（备选）

#### 创建 Bot

1. 在 Telegram 搜索 `@BotFather`
2. 发送 `/newbot` 创建机器人
3. 获取 Bot Token

#### 配置

```json
{
  "channels": {
    "telegram": {
      "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11",
      "webhookUrl": "https://your-domain.com/api/channels/telegram/webhook",
      "allowUsers": [],
      "allowGroups": []
    }
  }
}
```

---

## 第七部分：国内大模型配置 ⭐

### 通义千问（阿里云）

#### 获取 API Key

1. 登录 [阿里云 DashScope](https://dashscope.console.aliyun.com/apiKey)
2. 创建 API Key
3. 复制 Key（`sk-` 开头）

#### 配置

```json
{
  "models": {
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxxxxxxxxxxxxxxxx",
        "baseUrl": "https://dashscope.aliyuncs.com/api/v1"
      }
    },
    "models": {
      "qwen-max": {
        "provider": "dashscope",
        "model": "qwen-max",
        "cost": 0.04
      },
      "qwen-plus": {
        "provider": "dashscope",
        "model": "qwen-plus",
        "cost": 0.02
      }
    }
  }
}
```

---

### 文心一言（百度）

#### 获取 API Key

1. 登录 [百度千帆](https://console.bce.baidu.com/qianfan/)
2. 创建应用
3. 获取 API Key 和 Secret Key

#### 配置

```json
{
  "models": {
    "providers": {
      "qianfan": {
        "apiKey": "xxxxxxxxxxxxxxxxx",
        "secretKey": "xxxxxxxxxxxxxxxxx"
      }
    },
    "models": {
      "ernie-4.0": {
        "provider": "qianfan",
        "model": "ernie-4.0",
        "cost": 0.03
      },
      "ernie-3.5": {
        "provider": "qianfan",
        "model": "ernie-3.5",
        "cost": 0.01
      }
    }
  }
}
```

---

### 豆包（火山引擎）

#### 获取 API Key

1. 登录 [火山引擎](https://console.volcengine.com/iam/keymanage/)
2. 创建 Access Key
3. 获取 Access Key 和 Secret Key

#### 配置

```json
{
  "models": {
    "providers": {
      "volcengine": {
        "accessKey": "xxxxxxxxxxxxxxxxx",
        "secretKey": "xxxxxxxxxxxxxxxxx"
      }
    },
    "models": {
      "doubao-pro": {
        "provider": "volcengine",
        "model": "doubao-pro-4k",
        "cost": 0.02
      },
      "doubao-lite": {
        "provider": "volcengine",
        "model": "doubao-lite",
        "cost": 0.008
      }
    }
  }
}
```

---

### 讯飞星火

#### 获取 API Key

1. 登录 [讯飞开放平台](https://www.xfyun.cn/)
2. 创建应用
3. 获取 APPID、API Key 和 Secret Key

#### 配置

```json
{
  "models": {
    "providers": {
      "iflytek": {
        "appId": "xxxxxxxxxx",
        "apiKey": "xxxxxxxxxxxxxxxxx",
        "secretKey": "xxxxxxxxxxxxxxxxx"
      }
    },
    "models": {
      "spark-4.0": {
        "provider": "iflytek",
        "model": "spark-4.0",
        "cost": 0.03
      }
    }
  }
}
```

---

### Kimi（月之暗面）

#### 获取 API Key

1. 登录 [月之暗面开放平台](https://platform.moonshot.cn/)
2. 创建 API Key

#### 配置

```json
{
  "models": {
    "providers": {
      "moonshot": {
        "apiKey": "sk-xxxxxxxxxxxxxxxxx"
      }
    },
    "models": {
      "moonshot-v1-8k": {
        "provider": "moonshot",
        "model": "moonshot-v1-8k",
        "cost": 0.012
      },
      "moonshot-v1-32k": {
        "provider": "moonshot",
        "model": "moonshot-v1-32k",
        "cost": 0.024
      }
    }
  }
}
```

---

### 智谱 GLM

#### 获取 API Key

1. 登录 [智谱开放平台](https://open.bigmodel.cn/)
2. 创建 API Key

#### 配置

```json
{
  "models": {
    "providers": {
      "zhipu": {
        "apiKey": "xxxxxxxxxxxxxxxxx"
      }
    },
    "models": {
      "glm-4": {
        "provider": "zhipu",
        "model": "glm-4",
        "cost": 0.05
      },
      "glm-3-turbo": {
        "provider": "zhipu",
        "model": "glm-3-turbo",
        "cost": 0.01
      }
    }
  }
}
```

---

### 本地模型（Ollama）

#### 安装 Ollama

```bash
# 下载安装
curl -fsSL https://ollama.com/install.sh | sh

# 或使用国内镜像
curl -fsSL https://ollama.az.run/install.sh | sh
```

#### 下载模型

```bash
# Qwen2.5
ollama pull qwen2.5:7b

# Llama 3
ollama pull llama3:8b

# 查看已下载模型
ollama list
```

#### 配置

```json
{
  "models": {
    "providers": {
      "ollama": {
        "baseUrl": "http://127.0.0.1:11434"
      }
    },
    "models": {
      "qwen2.5-7b": {
        "provider": "ollama",
        "model": "qwen2.5:7b",
        "cost": 0
      }
    }
  }
}
```

---

## 第八部分：渠道配置（国际）

---

## 多通道详细配置 ⭐⭐⭐

### Telegram 配置

1. 打开 Telegram，搜索 `@BotFather`
2. 发送 `/newbot` 命令
3. 获取 Token

```yaml
channels:
  - name: telegram
    type: telegram
    enabled: true
    config:
      bot_token: ${TELEGRAM_BOT_TOKEN}
```

---

### Discord 配置

1. 访问 https://discord.com/developers/applications
2. 创建应用和 Bot
3. 获取 Token

```yaml
channels:
  - name: discord
    type: discord
    enabled: true
    config:
      bot_token: ${DISCORD_BOT_TOKEN}
```

---

### Slack 配置

1. 访问 https://api.slack.com/apps
2. 创建应用
3. 获取 Bot Token (xoxb-)

```yaml
channels:
  - name: slack
    type: slack
    enabled: true
    config:
      bot_token: ${SLACK_BOT_TOKEN}
```

---

### WhatsApp 配置

1. 访问 https://developers.facebook.com
2. 创建 Meta 应用
3. 获取 Phone Number ID 和 Token

```yaml
channels:
  - name: whatsapp
    type: whatsapp
    enabled: true
    config:
      phone_number_id: ${WHATSAPP_PHONE_ID}
      access_token: ${WHATSAPP_ACCESS_TOKEN}
```

---


### 支持的渠道列表

| 渠道 | 类型 | 状态 | 插件 |
|------|------|------|------|
| **Telegram** | 即时通讯 | ✅ 原生 | - |
| **Discord** | 社区 | ✅ 原生 | - |
| **Slack** | 企业协作 | ✅ 原生 | - |
| **WhatsApp** | 即时通讯 | ⚠️ 社区 | @openclaw/channel-whatsapp |
| **iMessage** | 即时通讯 | ⚠️ 实验 | @openclaw/channel-imessage |

---

### WhatsApp 配置

#### 安装插件

```bash
npm install -g @openclaw/channel-whatsapp
```

#### 配置

```json
{
  "channels": {
    "whatsapp": {
      "phoneNumber": "+1234567890",
      "businessAccountId": "xxxxxxxxxxxx",
      "accessToken": "xxxxxxxxxxxxxxxxx"
    }
  }
}
```

---

### Discord 配置

#### 创建 Bot

1. 登录 [Discord Developer Portal](https://discord.com/developers/applications)
2. 创建应用
3. 创建 Bot
4. 复制 Token

#### 配置

```json
{
  "channels": {
    "discord": {
      "botToken": "xxxxxxxxxxxxxxxxx",
      "clientId": "xxxxxxxxxxxx",
      "guildId": "xxxxxxxxxxxx"
    }
  }
}
```

---

### iMessage 配置

#### 安装插件

```bash
npm install -g @openclaw/channel-imessage
```

#### 配置（macOS）

```json
{
  "channels": {
    "imessage": {
      "appleId": "your@apple.com",
      "deviceId": "xxxxxxxxxxxx"
    }
  }
}
```

---

### 渠道路由规则

#### 路由配置示例

```json
{
  "routing": {
    "defaultAgent": "default",
    "rules": [
      {
        "name": "feishu-coding",
        "channel": "feishu",
        "pattern": ".*代码.*|.*编程.*",
        "agent": "coding-agent",
        "priority": 10
      },
      {
        "name": "telegram-support",
        "channel": "telegram",
        "agent": "support-agent",
        "priority": 5
      },
      {
        "name": "vip-user",
        "channel": "feishu",
        "userId": "ou_xxxxxxxxxxxxx",
        "agent": "vip-agent",
        "priority": 20
      }
    ]
  }
}
```

---

## 第九部分：核心概念

### Gateway（网关）

**定义**：OpenClaw 的核心服务进程，管理所有 Channel、Agent 和 Model 连接

**职责**：
- 启动和停止服务
- 管理配置文件
- 协调各组件通信
- 提供 HTTP API 和 Dashboard

---

### Agent（智能体）

**定义**：处理用户消息的 AI 助手实例

**配置项**：
- `model`: 使用的 AI 模型
- `systemPrompt`: 系统提示词
- `temperature`: 创造性参数（0-1）
- `maxTokens`: 最大输出长度
- `tools`: 可用的工具列表

---

### Session（会话）

**定义**：用户与 Agent 的对话历史

**数据结构**：
```json
{
  "sessionId": "feishu:ou_xxx:oc_xxx:1711180800",
  "messages": [
    {"role": "user", "content": "..."},
    {"role": "assistant", "content": "..."}
  ]
}
```

---

### Memory（记忆）

**定义**：长期存储和检索对话历史

**类型**：
- **短期记忆**：最近 N 条对话
- **长期记忆**：向量数据库存储
- **工作记忆**：当前会话上下文

---

### Workspace（工作区）

**定义**：Agent 的文件系统和工具环境

**包含**：
- 配置文件
- 工具脚本
- 临时文件
- 缓存数据

---

## 第十部分：Agent 与工具

---

## 技能系统开发 ⭐⭐⭐

### SKILL.md 规范

```yaml
name: my-skill
version: 1.0.0
description: 技能描述
author: Your Name
license: MIT

triggers:
  - keywords: ["关键词"]

inputs:
  - name: query
    type: string
    required: true

outputs:
  type: text

dependencies:
  - requests>=2.28.0

env_vars:
  - name: API_KEY
    required: true

permissions:
  - network_access: true
```

---

### 技能调用流程

```
用户消息 → Gateway → 意图识别 → 技能匹配 → 参数提取 → 技能执行 → 结果返回
```

#### 调用示例

```python
from copaw import SkillContext, SkillResponse

async def execute(ctx: SkillContext) -> SkillResponse:
    query = ctx.get_param("query")
    api_key = ctx.get_env("API_KEY")
    
    try:
        result = await call_api(query, api_key)
        return SkillResponse(success=True, data=result)
    except Exception as e:
        return SkillResponse(success=False, error=str(e))
```

---

### 完整示例：天气查询技能

```python
from copaw import SkillContext, SkillResponse
import requests

async def execute(ctx: SkillContext) -> SkillResponse:
    city = ctx.get_param("city")
    api_key = ctx.get_env("WEATHER_API_KEY")
    
    url = f"https://api.weather.com/conditions?city={city}"
    resp = requests.get(url, headers={"Authorization": f"Bearer {api_key}"})
    data = resp.json()
    
    return SkillResponse.success(f"# {city} 天气\n温度：{data['temp']}°C")
```

---


### Agent 工作区配置

```json
{
  "agents": {
    "coding-agent": {
      "workspace": "/opt/openclaw/agents/coding",
      "tools": ["code-interpreter", "file-reader"],
      "environment": {
        "PYTHONPATH": "/opt/openclaw/agents/coding/lib"
      }
    }
  }
}
```

---

### 工具与插件系统

#### 内置工具

| 工具 | 功能 | 示例 |
|------|------|------|
| `search` | 网络搜索 | 查询最新信息 |
| `calculator` | 数学计算 | 复杂运算 |
| `calendar` | 日历管理 | 创建日程 |
| `weather` | 天气查询 | 获取天气预报 |

#### 自定义工具

```javascript
// tools/my-tool.js
module.exports = {
  name: 'my-tool',
  description: '我的自定义工具',
  async execute(params) {
    // 工具逻辑
    return result;
  }
};
```

---

### MCP 协议集成

**MCP**（Model Context Protocol）是 AI 模型与外部工具通信的标准协议

#### 配置 MCP 服务器

```json
{
  "mcp": {
    "servers": [
      {
        "name": "filesystem",
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-filesystem", "/data"]
      }
    ]
  }
}
```

---

### 定时任务与自动化

#### 配置定时任务

```json
{
  "cron": {
    "jobs": [
      {
        "name": "daily-report",
        "schedule": "0 8 * * *",
        "agent": "report-agent",
        "message": "生成日报"
      }
    ]
  }
}
```

---

## 第十一部分：会话与记忆管理

### 会话管理深度解析

#### 会话生命周期

```
创建 → 活跃 → 休眠 → 归档 → 删除
```

#### 会话压缩

当会话超过阈值时自动压缩：

```json
{
  "memory": {
    "compression": {
      "enabled": true,
      "threshold": 50,
      "strategy": "summarize"
    }
  }
}
```

---

### 记忆系统架构

#### 向量记忆

```json
{
  "memory": {
    "vectorStore": {
      "provider": "chroma",
      "collection": "openclaw-memory",
      "dimensions": 768
    }
  }
}
```

---

### 会话压缩机制

#### 压缩策略

| 策略 | 说明 | 适用场景 |
|------|------|---------|
| `truncate` | 截断旧消息 | 简单对话 |
| `summarize` | AI 总结 | 长对话 |
| `hybrid` | 截断 + 总结 | 平衡性能 |

---

## 第十二部分：配置参考 ⭐

### 配置文件结构

```
~/.openclaw/
├── openclaw.json      # 主配置
├── agents/            # Agent 配置
│   └── default/
│       └── config.json
└── data/              # 数据目录
    ├── sessions.db
    └── memory/
```

---

### 环境变量参考

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `OPENCLAW_PORT` | 服务端口 | 3000 |
| `OPENCLAW_HOST` | 监听地址 | 0.0.0.0 |
| `OPENCLAW_LOG_LEVEL` | 日志级别 | info |
| `OPENCLAW_DATA_DIR` | 数据目录 | ~/.openclaw/data |

---

### 配置项详解

#### Gateway 配置

```json
{
  "gateway": {
    "port": 3000,
    "host": "0.0.0.0",
    "logLevel": "info",
    "dataDir": "~/.openclaw/data",
    "maxConnections": 100,
    "timeout": 30000
  }
}
```

---

### 配置模板

#### 最小配置

```json
{
  "gateway": {
    "port": 3000
  },
  "models": {
    "default": "qwen-max",
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxx"
      }
    }
  },
  "channels": {
    "feishu": {
      "appId": "cli_xxx",
      "appSecret": "xxx"
    }
  }
}
```

---

## 第十三部分：运维管理

### Gateway 运维管理

#### 健康检查

```bash
# HTTP 健康检查
curl http://localhost:3000/health

# 输出：{"status":"ok","uptime":86400}
```

---

### 日志与调试

#### 日志级别

| 级别 | 说明 | 使用场景 |
|------|------|---------|
| `debug` | 调试信息 | 开发调试 |
| `info` | 一般信息 | 生产环境 |
| `warn` | 警告信息 | 问题排查 |
| `error` | 错误信息 | 故障定位 |

---

### 监控与告警

#### Prometheus 指标

```bash
# 暴露指标端点
curl http://localhost:3000/metrics
```

---

### 备份与恢复

#### 备份配置

```bash
# 备份配置文件
cp ~/.openclaw/openclaw.json ~/.openclaw/openclaw.json.bak

# 备份数据
tar -czf openclaw-backup.tar.gz ~/.openclaw/data/
```

---

### 升级与迁移

#### 版本升级

```bash
# npm 升级
npm update -g openclaw

# Docker 升级
docker pull openclaw/openclaw:latest
docker stop openclaw && docker rm openclaw
docker run -d --name openclaw ...
```

---

## 第十四部分：安全与优化

---

## 安全与权限详解 ⭐⭐⭐

### 沙箱模式

```yaml
security:
  sandbox:
    enabled: true
    mode: strict  # strict | permissive | disabled
    
    filesystem:
      allowed_paths: [/home/user/openclaw/data]
      max_file_size: 10MB
    
    network:
      allowed_hosts: [api.openai.com]
      max_connections: 100
```

#### 模式对比

| 模式 | 文件访问 | 网络访问 | 进程执行 | 适用场景 |
|------|----------|----------|----------|----------|
| strict | 只读指定目录 | 仅白名单 | 禁止 | 生产 |
| permissive | 读写指定目录 | 白名单 + 本地 | 受限 | 开发 |
| disabled | 无限制 | 无限制 | 无限制 | 测试 |

---

### DM 安全策略

```yaml
security:
  dm_policy:
    allowed_users: [user_123]
    rate_limit:
      messages_per_minute: 10
    content_filter:
      block_keywords: ["密码", "token"]
```

---

### TCC 权限模型

- **Trust**: admin/developer/user
- **Capability**: 网络/文件/进程
- **Context**: 时间/地点/设备

---

### 敏感操作防护

```yaml
security:
  sensitive_ops:
    require_2fa: [delete_channel, export_data]
    audit_log:
      enabled: true
```

---


### 安全配置

#### API Key 保护

```bash
# 设置文件权限
chmod 600 ~/.openclaw/openclaw.json

# 使用环境变量
export DASHSCOPE_API_KEY=sk-xxx
```

---

### 性能优化

#### 缓存配置

```json
{
  "cache": {
    "enabled": true,
    "maxSize": 1000,
    "ttl": 3600
  }
}
```

---

### 高可用配置

#### 负载均衡

```nginx
upstream openclaw {
  server 192.168.1.10:3000;
  server 192.168.1.11:3000;
}

server {
  location / {
    proxy_pass http://openclaw;
  }
}
```

---

## 第十五部分：故障排查

### 诊断命令速查

```bash
# 检查服务状态
openclaw status

# 诊断工具
openclaw doctor

# 查看日志
openclaw logs --level error
```

---

### 网络问题排查

```bash
# 测试 API 连接
curl -I https://dashscope.aliyuncs.com/api/v1

# 检查 DNS
nslookup dashscope.aliyuncs.com
```

---

### 高频问题解决方案

| 问题 | 解决方案 |
|------|---------|
| 服务无法启动 | 检查端口占用：`netstat -tlnp | grep 3000` |
| 渠道连接失败 | 检查 Webhook URL 是否可访问 |
| 模型 API 报错 | 检查 API Key 是否有效 |
| 内存占用高 | 调整 `maxSessions` 参数 |

---


---

## 故障排查详解 ⭐⭐⭐

### 日志分析

#### 日志级别

| 级别 | 说明 | 使用场景 |
|------|------|----------|
| DEBUG | 调试信息 | 开发 |
| INFO | 一般信息 | 正常 |
| WARN | 警告 | 潜在问题 |
| ERROR | 错误 | 功能异常 |
| CRITICAL | 严重错误 | 系统崩溃 |

#### 查看日志

```bash
openclaw logs --follow        # 实时查看
openclaw logs --level error   # 查看错误
openclaw logs --lines 100     # 最近 100 行
```

---

### 常见问题

#### 1. 网关启动失败

```bash
netstat -tlnp | grep 8088
openclaw logs --level debug | tail -50
openclaw config validate
```

**解决**: 更换端口/杀掉进程/修复配置

---

#### 2. 通道连接异常

```bash
curl -I https://api.telegram.org
openclaw config view --key channels.telegram.bot_token
```

**解决**: 更新 Token/配置代理

---

#### 3. 权限不足

```bash
openclaw user grant <user_id> <permission>
```

---

#### 4. API 限流（429）

**解决**: 启用缓存/调整速率/切换模型

---

#### 5. 内存溢出

```bash
openclaw cache clear --older-than 1d
openclaw restart --graceful
```

---

### 诊断工具

```bash
openclaw doctor
openclaw doctor --check network
openclaw doctor --check config
```

---

## 附录 A：完整 CLI 命令参考

| 命令 | 功能 | 示例 |
|------|------|------|
| `openclaw start` | 启动服务 | `openclaw start --daemon` |
| `openclaw stop` | 停止服务 | `openclaw stop --force` |
| `openclaw restart` | 重启服务 | `openclaw restart` |
| `openclaw status` | 查看状态 | `openclaw status` |
| `openclaw onboarding` | 配置向导 | `openclaw onboarding` |
| `openclaw channel list` | 列出渠道 | `openclaw channel list` |
| `openclaw channel add` | 添加渠道 | `openclaw channel add telegram` |
| `openclaw channel test` | 测试渠道 | `openclaw channel test feishu` |
| `openclaw model list` | 列出模型 | `openclaw model list` |
| `openclaw model test` | 测试模型 | `openclaw model test qwen-max` |
| `openclaw agent list` | 列出 Agent | `openclaw agent list` |
| `openclaw config view` | 查看配置 | `openclaw config view` |
| `openclaw logs` | 查看日志 | `openclaw logs --level error` |
| `openclaw doctor` | 诊断工具 | `openclaw doctor` |
| `openclaw dashboard` | 打开面板 | `openclaw dashboard` |

---

## 附录 B：环境变量完整参考

### 核心环境变量

| 变量名 | 说明 | 默认值 | 示例 |
|--------|------|--------|------|
| `OPENCLAW_PORT` | Gateway 端口 | 3000 | 3000 |
| `OPENCLAW_HOST` | 监听地址 | 0.0.0.0 | 127.0.0.1 |
| `OPENCLAW_LOG_LEVEL` | 日志级别 | info | debug |
| `OPENCLAW_DATA_DIR` | 数据目录 | ~/.openclaw/data | /var/lib/openclaw |
| `OPENCLAW_CONFIG_FILE` | 配置文件路径 | ~/.openclaw/openclaw.json | /etc/openclaw/config.json |

### 模型 API Key

| 变量名 | 提供商 | 获取方式 |
|--------|--------|---------|
| `DASHSCOPE_API_KEY` | 阿里云通义千问 | https://dashscope.console.aliyun.com/apiKey |
| `QIANFAN_API_KEY` | 百度文心一言 | https://console.bce.baidu.com/qianfan/ |
| `QIANFAN_SECRET_KEY` | 百度文心一言 | 同上 |
| `VOLCENGINE_ACCESS_KEY` | 火山引擎豆包 | https://console.volcengine.com/iam/ |
| `VOLCENGINE_SECRET_KEY` | 火山引擎豆包 | 同上 |
| `OPENAI_API_KEY` | OpenAI | https://platform.openai.com/api-keys |
| `ANTHROPIC_API_KEY` | Anthropic | https://console.anthropic.com/settings/keys |

---

## 附录 C：配置文件完整参考

### 完整配置示例

```json
{
  "gateway": {
    "port": 3000,
    "host": "0.0.0.0",
    "logLevel": "info",
    "dataDir": "~/.openclaw/data"
  },
  "channels": {
    "feishu": {
      "appId": "cli_xxx",
      "appSecret": "xxx",
      "encryptKey": "xxx",
      "verificationToken": "xxx",
      "allowUsers": [],
      "allowGroups": [],
      "requireMention": true
    },
    "telegram": {
      "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11",
      "allowUsers": [],
      "allowGroups": []
    }
  },
  "models": {
    "default": "qwen-max",
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxx",
        "baseUrl": "https://dashscope.aliyuncs.com/api/v1"
      },
      "qianfan": {
        "apiKey": "xxx",
        "secretKey": "xxx"
      }
    },
    "fallbacks": [
      {
        "from": "qwen-max",
        "to": ["qwen-plus", "ernie-4.0"]
      }
    ]
  },
  "agents": {
    "default": {
      "model": "qwen-max",
      "systemPrompt": "你是一个有帮助的 AI 助手。",
      "temperature": 0.7,
      "maxTokens": 2048,
      "tools": []
    },
    "coding-agent": {
      "model": "qwen-max",
      "systemPrompt": "你是一个专业的编程助手。",
      "temperature": 0.3,
      "maxTokens": 4096,
      "tools": ["code-interpreter"]
    }
  },
  "routing": {
    "defaultAgent": "default",
    "rules": [
      {
        "name": "coding",
        "pattern": ".*代码.*|.*编程.*",
        "agent": "coding-agent",
        "priority": 10
      }
    ]
  },
  "memory": {
    "enabled": true,
    "maxSessions": 100,
    "maxMessagesPerSession": 50,
    "vectorStore": {
      "provider": "local",
      "dimensions": 768
    }
  }
}
```

---

## 附录 D：国内 API Key 获取指南

### 阿里云 DashScope

1. 访问 https://dashscope.console.aliyun.com/
2. 登录阿里云账号
3. 进入"API-KEY 管理"
4. 创建新 API Key
5. 复制并保存（仅显示一次）

### 百度千帆

1. 访问 https://console.bce.baidu.com/qianfan/
2. 登录百度账号
3. 进入"应用接入"
4. 创建应用
5. 获取 API Key 和 Secret Key

### 火山引擎

1. 访问 https://console.volcengine.com/
2. 登录火山引擎账号
3. 进入"IAM-访问密钥"
4. 创建 Access Key
5. 获取 Access Key 和 Secret Key

---

## 附录 E：架构决策记录

### 为什么选择 Node.js？

- **性能**：事件驱动、非阻塞 I/O
- **生态**：丰富的 npm 包
- **跨平台**：Windows/Linux/macOS 统一体验

### 为什么支持多渠道？

- **用户需求**：不同企业使用不同平台
- **灵活性**：不绑定单一平台
- **扩展性**：易于添加新渠道

### 为什么自托管？

- **数据隐私**：数据完全本地控制
- **成本**：仅支付 API 费用
- **定制**：可深度定制和扩展

---

**文档版本**: v6.0 完整版  
**最后更新**: 2026-03-23  
**官方文档**: https://docs.openclaw.ai/  
**GitHub**: https://github.com/openclaw/openclaw
