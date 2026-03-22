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

（保留之前的本土化内容，包括国内网络环境适配、国内大模型接入、国内聊天平台配置、镜像加速方案等）

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

（文档继续...）
