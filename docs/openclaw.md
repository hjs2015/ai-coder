# 🦞 OpenClaw 官方完全指南

> **自托管 AI 网关 · 连接任何聊天应用到 AI Agent**  
> **文档版本**: v3.0 完整版（基于官方文档 2026-03-22）  
> **官方文档**: https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **Discord**: https://discord.com/invite/clawd  
> **许可证**: MIT  
> **最后更新**: 2026-03-23

---

## 📑 完整目录

<details>
<summary><b>点击展开完整目录（9 大部分 52 章节）</b></summary>

### 第一部分：产品认知与入门
1. [什么是 OpenClaw](#什么是-openclaw)
2. [核心价值与定位](#核心价值与定位)
3. [适用场景](#适用场景)
4. [与其他方案对比](#与其他方案对比)
5. [核心术语对照表](#核心术语对照表)
6. [系统要求与兼容矩阵](#系统要求与兼容矩阵)
7. [硬件配置建议](#硬件配置建议)

### 第二部分：快速开始
8. [5 分钟快速安装](#5-分钟快速安装)
9. [Onboarding 概述](#onboarding-概述)
10. [CLI Onboarding 详细步骤](#cli-onboarding-详细步骤)
11. [macOS App Onboarding](#macos-app-onboarding)
12. [验证安装](#验证安装)

### 第三部分：安装与部署
13. [Node.js 安装指南](#nodejs-安装指南)
14. [npm 全局安装](#npm-全局安装)
15. [Docker 容器化部署](#docker-容器化部署)
16. [Docker Compose 部署](#docker-compose-部署)
17. [源码安装](#源码安装)
18. [离线安装](#离线安装)
19. [多实例部署](#多实例部署)

### 第四部分：渠道配置
20. [支持的渠道列表](#支持的渠道列表)
21. [Telegram 配置（推荐）](#telegram-配置推荐)
22. [WhatsApp 配置](#whatsapp-配置)
23. [Discord 配置](#discord-配置)
24. [iMessage 配置（BlueBubbles）](#imessage-配置 bluebubbles)
25. [飞书配置](#飞书配置)
26. [Slack 配置](#slack-配置)
27. [渠道路由规则](#渠道路由规则)
28. [群组消息配置](#群组消息配置)

### 第五部分：模型配置
29. [模型选择指南](#模型选择指南)
30. [模型提供商目录](#模型提供商目录)
31. [API Key 配置](#api-key-配置)
32. [模型故障转移](#模型故障转移)
33. [Token 使用与成本优化](#token-使用与成本优化)
34. [提示词缓存](#提示词缓存)

### 第六部分：配置参考
35. [配置文件位置](#配置文件位置)
36. [配置键详解](#配置键详解)
37. [访问控制配置](#访问控制配置)
38. [环境变量配置](#环境变量配置)
39. [配置模板](#配置模板)

### 第七部分：运维与监控
40. [服务管理](#服务管理)
41. [日志查看](#日志查看)
42. [性能监控](#性能监控)
43. [备份与恢复](#备份与恢复)
44. [升级指南](#升级指南)
45. [故障排查](#故障排查)

### 第八部分：安全与生产
46. [安全最佳实践](#安全最佳实践)
47. [生产环境部署](#生产环境部署)
48. [高可用配置](#高可用配置)
49. [数据隐私保护](#数据隐私保护)

### 第九部分：开发与贡献
50. [开发环境搭建](#开发环境搭建)
51. [插件开发](#插件开发)
52. [贡献指南](#贡献指南)

### 附录
- [CLI 命令速查](#cli-命令速查)
- [常见问题 FAQ](#常见问题-faq)
- [资源链接](#资源链接)

</details>

---

## 第一部分：产品认知与入门

### 什么是 OpenClaw

**OpenClaw** 是一个**自托管 AI 网关**，将任何聊天应用连接到 AI Agent。

> "EXFOLIATE! EXFOLIATE!" — A space lobster, probably

#### 核心定位

```
┌──────────────────┐
│  聊天应用         │
│  + 插件扩展       │
└─────────────────┘
         │
         ↓
┌──────────────────┐
│    Gateway       │
│   (OpenClaw)     │ ← 自托管在你的服务器
└────────┬─────────┘
         │
    ┌────┴────┬─────────┬──────────┐
    ↓         ↓         ↓          ↓
┌──────┐ ┌──────┐ ┌────────┐ ┌─────────┐
│PI    │ │ CLI  │ │Web UI  │ │Mobile   │
│Agent │ │      │ │        │ │Nodes    │
└──────┘ └──────┘ └────────┘ └─────────┘
         │
    ┌────┴────┬─────────┬──────────┐
    ↓         ↓         ↓          ↓
┌──────┐ ┌──────┐ ┌────────┐ ┌─────────┐
│Claude│ │GPT   │ │Gemini  │ │其他模型 │
└──────┘ └──────┘ └────────┘ └─────────┘
```

**网关是所有会话、路由和渠道连接的单一事实来源。**

---

### 核心价值与定位

#### 自托管 AI 网关的核心优势

| 特性 | OpenClaw | 托管式 AI 助手 | 传统聊天机器人 |
|------|----------|--------------|--------------|
| **数据控制** | ✅ 完全本地控制 | ❌ 数据在第三方 | ⚠️ 部分控制 |
| **隐私保护** | ✅ 数据不出服务器 | ❌ 数据上传云端 | ⚠️ 依赖服务商 |
| **自定义程度** | ✅ 完全可定制 | ❌ 固定功能 | ⚠️ 有限定制 |
| **成本** | ✅ 仅支付 API 费用 | ❌ 订阅费 +API 费 | ⚠️ 按量付费 |
| **集成灵活性** | ✅ 支持 30+ 渠道 | ❌ 固定渠道 | ⚠️ 有限集成 |
| **离线运行** | ✅ 支持本地模型 | ❌ 必须联网 | ❌ 必须联网 |
| **多 Agent 协作** | ✅ 原生支持 | ❌ 单 Agent | ❌ 单 Agent |

#### 与同类开源方案对比

| 特性 | OpenClaw | Botpress | Rasa | LangChain |
|------|----------|----------|------|-----------|
| **定位** | AI 网关 | 聊天机器人平台 | 对话框架 | AI 应用框架 |
| **部署难度** | ⭐⭐ 简单 | ⭐⭐⭐ 中等 | ⭐⭐⭐⭐ 复杂 | ⭐⭐⭐ 中等 |
| **渠道支持** | 30+ | 20+ | 15+ | 依赖集成 |
| **多 Agent** | ✅ 原生 | ⚠️ 需配置 | ❌ 不支持 | ✅ 需开发 |
| **自托管** | ✅ 完全 | ✅ 完全 | ✅ 完全 | ✅ 完全 |
| **学习曲线** | ⭐⭐ 低 | ⭐⭐⭐ 中 | ⭐⭐⭐⭐ 高 | ⭐⭐⭐ 中 |

---

### 适用场景

#### 1. 个人远程编码助手

**场景描述**：开发者通过微信/Telegram 随时随地与 AI 协作编程

**核心价值**：
- 无需打开电脑，手机即可代码审查
- 通勤路上处理紧急 Bug
- 多设备无缝切换

**配置建议**：
- 渠道：Telegram/微信
- 模型：Claude Sonnet（代码能力强）
- 工具：代码执行插件

**适用人群**：软件工程师、全栈开发者

---

#### 2. 多设备 AI 协同

**场景描述**：在手机、平板、电脑、智能手表上访问同一 AI 助手

**核心价值**：
- 会话同步，随时随地继续对话
- 不同设备不同交互方式
- 统一配置管理

**配置建议**：
- 渠道：Telegram + Discord + Web
- 会话：每发送者独立会话
- 同步：启用云端会话存储

**适用人群**：多设备用户、数字游民

---

#### 3. 自动化运维

**场景描述**：通过聊天应用接收服务器告警、执行运维命令

**核心价值**：
- 7×24 小时监控告警
- 一键执行运维脚本
- 自动记录操作日志

**配置建议**：
- 渠道：Telegram（支持命令）
- 工具：SSH 执行插件
- 安全：IP 白名单 + 命令审计

**适用人群**：运维工程师、SRE

---

#### 4. 团队轻量 AI 助手

**场景描述**：小团队无需复杂系统，通过 Slack/飞书快速接入 AI

**核心价值**：
- 5 分钟部署，零学习成本
- 团队共享 AI 能力
- 按需分配额度

**配置建议**：
- 渠道：Slack/飞书
- 模型：按团队需求选择
- 配额：设置团队额度上限

**适用人群**：初创团队、项目组

---

#### 5. 7×24 小时离线 AI 任务

**场景描述**：定时任务、后台处理、批量操作

**核心价值**：
- 无需人工值守
- 自动执行重复任务
- 结果推送通知

**配置建议**：
- 渠道：Telegram（推送通知）
- 定时：Cron 表达式
- 日志：详细执行记录

**适用人群**：数据分析师、自动化工程师

---

### 与其他方案对比

#### 传统 AI 聊天工具 vs OpenClaw

| 维度 | 传统 AI 聊天工具 | OpenClaw |
|------|----------------|----------|
| **部署方式** | SaaS 云端 | 自托管 |
| **数据归属** | 平台所有 | 用户所有 |
| **定制能力** | 有限 | 完全定制 |
| **集成成本** | 低（但受限） | 中（但灵活） |
| **长期成本** | 高（订阅费） | 低（仅 API） |
| **隐私风险** | 高 | 低 |

#### 何时选择 OpenClaw

✅ **适合使用 OpenClaw**：
- 需要数据完全控制
- 需要集成多个聊天渠道
- 需要自定义 Agent 行为
- 需要多 Agent 协作
- 关注长期成本

❌ **不适合 OpenClaw**：
- 只需简单聊天机器人
- 无自托管能力
- 只需单一渠道
- 需要开箱即用的复杂功能

---

### 核心术语对照表

| 术语 | 英文 | 定义 | 示例 |
|------|------|------|------|
| **网关** | Gateway | OpenClaw 核心服务，管理所有连接和会话 | `openclaw start` 启动的服务 |
| **渠道** | Channel | 聊天应用连接器，如 Telegram、WhatsApp | Telegram Bot、WhatsApp Business |
| **Agent** | Agent | AI 代理，负责处理消息和调用工具 | Pi Agent、自定义 Agent |
| **会话** | Session | 单个用户与 Agent 的对话上下文 | 每个 Telegram 用户独立会话 |
| **节点** | Node | 移动设备或浏览器端的连接点 | iOS Node、Web Node |
| **RPC 模式** | RPC Mode | 内部进程通信模式，高性能低延迟 | 默认通信方式 |
| **Pi Agent** | Pi Agent | OpenClaw 内置的 AI Agent | 捆绑的二进制文件 |
| **Onboarding** | Onboarding | 初次配置向导 | `openclaw onboard` |
| **Dashboard** | Dashboard | Web 控制界面 | `openclaw dashboard` 打开的页面 |
| **工具** | Tool | Agent 可调用的功能 | 文件读写、命令执行 |
| **插件** | Plugin | 扩展渠道或工具 | Mattermost 插件 |
| **技能** | Skill | 预定义的 Agent 能力 | 代码审查、文档生成 |

---

### 系统要求与兼容矩阵

#### Node.js 版本兼容

| Node.js 版本 | 兼容性 | 备注 |
|-------------|--------|------|
| **Node 24.x** | ✅ 推荐 | 最新 LTS，性能最优 |
| **Node 22.16+** | ✅ 支持 | 最低要求版本 |
| **Node 20.x** | ⚠️ 部分支持 | 可能缺少新功能 |
| **Node 18.x** | ❌ 不支持 | 版本过低 |

**检查 Node 版本**：
```bash
node --version
# 输出：v24.x.x
```

#### 操作系统兼容

| 操作系统 | 版本要求 | 支持状态 | 备注 |
|---------|---------|---------|------|
| **macOS** | 12.0+ (Monterey) | ✅ 完全支持 | 推荐 macOS 14+ |
| **Ubuntu** | 20.04+ | ✅ 完全支持 | 推荐 22.04 LTS |
| **Debian** | 11+ (Bullseye) | ✅ 完全支持 | 推荐 12 (Bookworm) |
| **CentOS** | 8+ | ✅ 完全支持 | 注意 8 已 EOL |
| **RHEL** | 8+ | ✅ 完全支持 | 企业推荐 |
| **Windows** | 10/11 | ✅ 支持 | 原生或 WSL2 |
| **WSL2** | Windows 10 2004+ | ✅ 推荐 | 性能接近原生 Linux |

#### CPU 架构支持

| 架构 | 支持状态 | 备注 |
|------|---------|------|
| **x86_64** | ✅ 完全支持 | Intel/AMD 处理器 |
| **ARM64** | ✅ 完全支持 | Apple Silicon、树莓派 4 |
| **ARMv7** | ⚠️ 部分支持 | 树莓派 3，性能有限 |

---

### 硬件配置建议

#### 最低配置

| 组件 | 要求 | 说明 |
|------|------|------|
| **CPU** | 1 核心 | 单用户轻量使用 |
| **内存** | 512MB | 仅网关，无本地模型 |
| **存储** | 1GB | 程序 + 配置 + 日志 |
| **网络** | 1Mbps | 基础聊天消息 |

**适用场景**：个人测试、单用户、简单聊天

---

#### 推荐配置（个人使用）

| 组件 | 要求 | 说明 |
|------|------|------|
| **CPU** | 2 核心 | 多用户并发 |
| **内存** | 2GB | 流畅运行 + 缓存 |
| **存储** | 5GB | 日志 + 会话历史 |
| **网络** | 10Mbps | 媒体消息传输 |

**适用场景**：个人生产使用、小团队

---

#### 推荐配置（团队使用）

| 组件 | 要求 | 说明 |
|------|------|------|
| **CPU** | 4 核心 | 高并发 |
| **内存** | 8GB | 多 Agent + 缓存 |
| **存储** | 20GB SSD | 快速读写 |
| **网络** | 100Mbps | 企业级带宽 |

**适用场景**：团队生产环境、多用户

---

#### 前置依赖

| 依赖 | 必需 | 用途 | 安装命令 |
|------|------|------|---------|
| **Node.js** | ✅ | 运行环境 | 见安装指南 |
| **npm** | ✅ | 包管理 | 随 Node.js 安装 |
| **Git** | ⚠️ | 源码安装/插件 | `apt install git` |
| **Docker** | ⚠️ | 容器化部署 | `apt install docker.io` |
| **systemd** | ⚠️ | 服务管理 | 大多数 Linux 自带 |

---

## 第二部分：快速开始

### 5 分钟快速安装

#### 步骤 1：安装 Node.js（如未安装）

**macOS**：
```bash
# 使用 Homebrew
brew install node@24
```

**Ubuntu/Debian**：
```bash
# 使用 NodeSource
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Windows**：
```bash
# 下载安装 https://nodejs.org/
# 或使用 winget
winget install OpenJS.NodeJS.LTS
```

**验证安装**：
```bash
node --version
# 输出：v24.x.x

npm --version
# 输出：10.x.x
```

---

#### 步骤 2：安装 OpenClaw

```bash
npm install -g openclaw@latest
```

**验证安装**：
```bash
openclaw --version
# 输出：openclaw/x.x.x
```

---

#### 步骤 3：运行 Onboarding

```bash
openclaw onboard
```

**配置流程**：
1. 选择模型提供商（Anthropic/OpenAI/Google 等）
2. 输入 API Key
3. 选择渠道（推荐 Telegram）
4. 安装系统服务（可选）

---

#### 步骤 4：打开 Dashboard

```bash
openclaw dashboard
```

浏览器自动打开 `http://localhost:18789`

---

#### 步骤 5：开始聊天

- **方式 1**：在 Dashboard 聊天界面发送消息
- **方式 2**：通过配置的渠道（如 Telegram）发送消息

---

### Onboarding 概述

OpenClaw 有两个 Onboarding 路径，都配置认证、网关和可选渠道——区别在于交互方式。

#### 选择指南

| 特性 | CLI Onboarding | macOS App Onboarding |
|------|---------------|---------------------|
| **平台** | macOS, Linux, Windows | macOS only |
| **界面** | 终端向导 | 应用内引导 UI |
| **最佳场景** | 服务器、无头、完全控制 | 桌面用户、图形界面偏好 |
| **配置灵活性** | ⭐⭐⭐⭐⭐ 完全控制 | ⭐⭐⭐ 预设选项 |
| **安装时间** | ~5 分钟 | ~3 分钟 |

---

### CLI Onboarding 详细步骤

#### 运行 Onboarding

```bash
openclaw onboard
```

#### 配置步骤详解

**步骤 1：选择模型提供商**

```
? Select a model provider:
  ❯ Anthropic (Claude)
    OpenAI (GPT)
    Google (Gemini)
    xAI (Grok)
    Other...
```

**推荐**：Anthropic Claude（代码能力强）

---

**步骤 2：输入 API Key**

```
? Enter your Anthropic API key:
  [隐藏输入]
```

**获取 API Key**：
- Anthropic: https://console.anthropic.com/
- OpenAI: https://platform.openai.com/api-keys
- Google: https://makersuite.google.com/app/apikey

**安全提示**：
- API Key 仅存储在本地配置文件
- 不会上传到 OpenClaw 服务器
- 建议创建专用 Key（非主账户 Key）

---

**步骤 3：选择渠道**

```
? Configure a channel (optional):
  ❯ Telegram (recommended)
    WhatsApp
    Discord
    iMessage (requires macOS)
    Skip (configure later)
```

**推荐**：Telegram（最简单，5 分钟完成）

---

**步骤 4：配置 Telegram（如选择）**

1. **创建 Bot**：
   - 在 Telegram 中搜索 `@BotFather`
   - 发送 `/newbot`
   - 输入 Bot 名称和用户名
   - 获取 Bot Token

2. **输入 Token**：
   ```
   ? Enter your Telegram Bot Token:
     [粘贴 Token]
   ```

3. **测试连接**：
   - 在 Telegram 中搜索你的 Bot
   - 发送 `/start`
   - 收到回复表示成功

---

**步骤 5：安装系统服务**

```
? Install as a system service? (recommended)
  ❯ Yes
    No
```

**推荐**：Yes（开机自启，后台运行）

---

### macOS App Onboarding

#### 下载与安装

1. 访问 https://github.com/openclaw/openclaw/releases
2. 下载 macOS 应用
3. 拖拽到 Applications 文件夹
4. 打开应用

#### 配置流程

1. **欢迎界面** → 点击 "Get Started"
2. **选择模型提供商** → 点击图标
3. **输入 API Key** → 粘贴并保存
4. **选择渠道** → 按向导配置
5. **完成** → 开始聊天

---

### 验证安装

#### 检查服务状态

```bash
# 查看状态
openclaw status

# 输出示例：
# OpenClaw Gateway: running
# Dashboard: http://localhost:18789
# Channels: telegram (connected)
```

---

#### 查看日志

```bash
# 实时日志
openclaw logs

# 最近 100 行
openclaw logs --lines 100

# 过滤错误
openclaw logs | grep ERROR
```

---

#### 测试聊天

**方式 1：Dashboard**
```bash
openclaw dashboard
```
在浏览器中打开聊天界面，发送消息测试。

**方式 2：渠道**
在配置的渠道（如 Telegram）中发送消息，应收到 AI 回复。

---

#### 诊断问题

```bash
# 运行诊断
openclaw doctor

# 检查配置
openclaw config check

# 测试模型连接
openclaw models test
```

---

## 第三部分：安装与部署

### Node.js 安装指南

#### macOS 安装

**方法 1：Homebrew（推荐）**
```bash
# 安装 Homebrew（如未安装）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装 Node.js 24
brew install node@24

# 验证
node --version
npm --version
```

**方法 2：官方安装包**
1. 访问 https://nodejs.org/
2. 下载 macOS 安装包
3. 双击安装

---

#### Ubuntu/Debian 安装

**方法 1：NodeSource（推荐）**
```bash
# 安装 Node.js 24
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
sudo apt-get install -y nodejs

# 验证
node --version
npm --version
```

**方法 2：Snap**
```bash
sudo snap install node --classic
```

---

#### Windows 安装

**方法 1：官方安装包（推荐）**
1. 访问 https://nodejs.org/
2. 下载 Windows 安装包 (.msi)
3. 双击安装，按向导完成

**方法 2：Winget**
```powershell
winget install OpenJS.NodeJS.LTS
```

**方法 3：WSL2**
```bash
# 在 WSL2 中安装
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
sudo apt-get install -y nodejs
```

---

#### 国内镜像加速

**使用淘宝镜像**：
```bash
# 配置 npm 镜像
npm config set registry https://registry.npmmirror.com

# 验证
npm config get registry
```

**使用 nvm 管理版本**：
```bash
# 安装 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# 安装 Node.js 24
nvm install 24
nvm use 24
nvm alias default 24
```

---

### npm 全局安装

#### 标准安装

```bash
# 安装最新版
npm install -g openclaw@latest

# 安装指定版本
npm install -g openclaw@0.1.0

# 验证安装
openclaw --version
```

---

#### 国内加速安装

```bash
# 使用淘宝镜像
npm install -g openclaw@latest --registry=https://registry.npmmirror.com

# 或使用 cnpm
npm install -g cnpm --registry=https://registry.npmmirror.com
cnpm install -g openclaw@latest
```

---

#### 权限问题解决

**macOS/Linux 遇到权限错误**：

```bash
# 方案 1：使用 sudo（不推荐）
sudo npm install -g openclaw@latest

# 方案 2：修复 npm 权限（推荐）
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
npm install -g openclaw@latest
```

---

### Docker 容器化部署

#### 快速启动

```bash
docker run -d \
  --name openclaw \
  -p 18789:18789 \
  -v openclaw-data:/root/.openclaw \
  -e ANTHROPIC_API_KEY=sk-ant-xxx \
  ghcr.io/openclaw/openclaw:latest
```

---

#### 参数说明

| 参数 | 说明 | 示例 |
|------|------|------|
| `-d` | 后台运行 | - |
| `--name` | 容器名称 | openclaw |
| `-p` | 端口映射 | 18789:18789 |
| `-v` | 数据卷挂载 | openclaw-data:/root/.openclaw |
| `-e` | 环境变量 | ANTHROPIC_API_KEY=xxx |

---

#### 查看日志

```bash
# 实时日志
docker logs -f openclaw

# 最近 100 行
docker logs --tail 100 openclaw
```

---

#### 进入容器

```bash
# 进入容器 shell
docker exec -it openclaw bash

# 运行命令
docker exec openclaw openclaw status
```

---

#### 停止与删除

```bash
# 停止
docker stop openclaw

# 启动
docker start openclaw

# 删除容器
docker rm openclaw

# 删除数据卷（谨慎！）
docker volume rm openclaw-data
```

---

### Docker Compose 部署

#### 创建 docker-compose.yml

```yaml
version: '3.8'

services:
  openclaw:
    image: ghcr.io/openclaw/openclaw:latest
    container_name: openclaw
    restart: unless-stopped
    ports:
      - "18789:18789"
    volumes:
      - openclaw-data:/root/.openclaw
      - ./config:/root/.openclaw/config:ro
    environment:
      - ANTHROPIC_API_KEY=${ANTHROPIC_API_KEY}
      - OPENCLAW_PORT=18789
      - OPENCLAW_HOST=0.0.0.0
    networks:
      - openclaw-net

volumes:
  openclaw-data:

networks:
  openclaw-net:
    driver: bridge
```

---

#### 环境变量文件

创建 `.env` 文件：
```bash
# API Keys
ANTHROPIC_API_KEY=sk-ant-xxx
OPENAI_API_KEY=sk-xxx

# 配置
OPENCLAW_PORT=18789
OPENCLAW_HOST=0.0.0.0
OPENCLAW_LOG_LEVEL=info
```

---

#### 启动服务

```bash
# 启动
docker-compose up -d

# 查看状态
docker-compose ps

# 查看日志
docker-compose logs -f

# 停止
docker-compose down

# 重启
docker-compose restart
```

---

#### 多服务部署

```yaml
version: '3.8'

services:
  openclaw:
    image: ghcr.io/openclaw/openclaw:latest
    depends_on:
      - redis
    environment:
      - REDIS_URL=redis://redis:6379

  redis:
    image: redis:7-alpine
    volumes:
      - redis-data:/data

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf

volumes:
  redis-data:
```

---

### 源码安装

#### 克隆仓库

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
```

---

#### 安装依赖

```bash
# 安装依赖
npm install

# 开发模式安装
npm install --dev
```

---

#### 构建

```bash
# 构建生产版本
npm run build

# 开发模式
npm run dev
```

---

#### 运行

```bash
# 开发模式运行
npm start

# 生产模式运行
npm run start:prod
```

---

#### 全局链接

```bash
# 创建全局链接
npm link

# 验证
openclaw --version
```

---

### 离线安装

#### 准备离线包

**在有网络的机器上**：
```bash
# 下载 tarball
npm pack openclaw@latest
# 输出：openclaw-x.x.x.tgz

# 下载依赖
npm install openclaw@latest --package-lock-only
```

---

#### 传输到离线机器

```bash
# 使用 U 盘或 scp 传输
scp openclaw-x.x.x.tgz user@offline-server:/tmp/
```

---

#### 离线安装

```bash
# 安装
npm install -g /tmp/openclaw-x.x.x.tgz

# 验证
openclaw --version
```

---

### 多实例部署

#### 场景说明

**为什么需要多实例**：
- 隔离不同环境（开发/测试/生产）
- 多租户隔离
- 不同配置测试

---

#### 配置多实例

**实例 1：开发环境**
```bash
# 创建配置目录
mkdir -p ~/.openclaw-dev

# 设置环境变量
export OPENCLAW_CONFIG_DIR=~/.openclaw-dev
export OPENCLAW_PORT=18790

# 启动
openclaw start
```

---

**实例 2：生产环境**
```bash
# 创建配置目录
mkdir -p ~/.openclaw-prod

# 设置环境变量
export OPENCLAW_CONFIG_DIR=~/.openclaw-prod
export OPENCLAW_PORT=18789

# 启动
openclaw start
```

---

#### 使用 systemd 管理多实例

**创建服务文件**：
```ini
# /etc/systemd/system/openclaw-dev.service
[Unit]
Description=OpenClaw Gateway (Development)
After=network.target

[Service]
Type=simple
User=devuser
Environment=OPENCLAW_CONFIG_DIR=/home/devuser/.openclaw-dev
Environment=OPENCLAW_PORT=18790
ExecStart=/usr/bin/openclaw start
Restart=always

[Install]
WantedBy=multi-user.target
```

```ini
# /etc/systemd/system/openclaw-prod.service
[Unit]
Description=OpenClaw Gateway (Production)
After=network.target

[Service]
Type=simple
User=produser
Environment=OPENCLAW_CONFIG_DIR=/home/produser/.openclaw-prod
Environment=OPENCLAW_PORT=18789
ExecStart=/usr/bin/openclaw start
Restart=always

[Install]
WantedBy=multi-user.target
```

---

**启动服务**：
```bash
# 重载 systemd
sudo systemctl daemon-reload

# 启动实例
sudo systemctl start openclaw-dev
sudo systemctl start openclaw-prod

# 查看状态
sudo systemctl status openclaw-dev
sudo systemctl status openclaw-prod
```

---

## 第四部分：渠道配置

### 支持的渠道列表

#### 消息平台（30+）

| 渠道 | 状态 | 配置难度 | 媒体支持 | 群组支持 |
|------|------|---------|---------|---------|
| **Telegram** | ✅ 生产就绪 | ⭐ 最简单 | ✅ 完整 | ✅ 完整 |
| **WhatsApp** | ✅ 生产就绪 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Discord** | ✅ 生产就绪 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **iMessage** | ✅ BlueBubbles | ⭐⭐⭐ 需 macOS | ✅ 完整 | ✅ 完整 |
| **Signal** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ⚠️ 有限 |
| **Slack** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **飞书** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Microsoft Teams** | ✅ 支持 | ⭐⭐⭐ 复杂 | ✅ 完整 | ✅ 完整 |
| **Google Chat** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Matrix** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Mattermost** | 🔌 插件 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **IRC** | ✅ 支持 | ⭐ 简单 | ⚠️ 文本 | ✅ 完整 |
| **LINE** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Nextcloud Talk** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Synology Chat** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Zalo** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Nostr** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Tlon** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ✅ 完整 |
| **Twitch** | ✅ 支持 | ⭐⭐ 中等 | ✅ 完整 | ⚠️ 有限 |

---

#### 特殊渠道

| 渠道 | 类型 | 说明 |
|------|------|------|
| **Voice Call Plugin** | 语音通话 | 实时语音交互 |
| **BlueBubbles** | iMessage 桥接 | macOS 服务器 REST API |

---

### Telegram 配置（推荐）

#### 为什么推荐 Telegram

- ✅ **配置最简单**：5 分钟完成
- ✅ **完全免费**：无 API 费用
- ✅ **功能完整**：支持文本、媒体、文件、语音
- ✅ **隐私保护**：端到端加密（私密聊天）
- ✅ **跨平台**：所有主流平台支持

---

#### 快速配置（5 分钟）

**步骤 1：创建 Bot**

1. 在 Telegram 中搜索 `@BotFather`
2. 发送 `/newbot`
3. 输入 Bot 名称（如：My AI Assistant）
4. 输入 Bot 用户名（如：my_ai_bot）
5. 获取 Bot Token（格式：`123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`）

---

**步骤 2：配置 OpenClaw**

```bash
# 编辑配置文件
nano ~/.openclaw/openclaw.json
```

添加配置：
```json
{
  "channels": {
    "telegram": {
      "botToken": "YOUR_BOT_TOKEN"
    }
  }
}
```

---

**步骤 3：重启服务**

```bash
openclaw restart
```

---

**步骤 4：测试连接**

1. 在 Telegram 中搜索你的 Bot 用户名
2. 点击 "Start" 或发送 `/start`
3. 收到欢迎消息表示成功

---

#### 高级配置

**访问控制**：
```json
{
  "channels": {
    "telegram": {
      "botToken": "YOUR_BOT_TOKEN",
      "allowFrom": ["123456789", "987654321"],
      "allowGroups": ["-1001234567890"],
      "requireMention": false
    }
  }
}
```

| 配置项 | 说明 | 示例 |
|--------|------|------|
| `allowFrom` | 允许的用户 ID 列表 | `["123456789"]` |
| `allowGroups` | 允许的群组 ID 列表 | `["-1001234567890"]` |
| `requireMention` | 群组中是否需要 @提及 | `true/false` |

---

**查找用户/群组 ID**：

1. **用户 ID**：
   - 发送消息给 @userinfobot
   - 或查看日志：`openclaw logs | grep user_id`

2. **群组 ID**：
   - 将 Bot 添加到群组
   - 发送消息
   - 查看日志获取群组 ID（负数）

---

**群组配置**：
```json
{
  "channels": {
    "telegram": {
      "groups": {
        "*": {
          "requireMention": true,
          "mentionPatterns": ["@bot", "@assistant"]
        },
        "-1001234567890": {
          "requireMention": false
        }
      }
    }
  }
}
```

---

#### 功能参考

| 功能 | 支持状态 | 说明 |
|------|---------|------|
| 文本消息 | ✅ | 完整支持 |
| 图片 | ✅ | 发送和接收 |
| 音频 | ✅ | 发送和接收 |
| 视频 | ✅ | 发送和接收 |
| 文档 | ✅ | 发送和接收 |
| 语音消息 | ✅ | 发送和接收 |
| 回复线程 | ✅ | 保持对话上下文 |
| 群组消息 | ✅ | 支持群聊 |
| 频道消息 | ✅ | 支持频道 |
| 命令 | ✅ | 支持 Bot 命令 |

---

### WhatsApp 配置

#### 配置方式

- 通过 QR 码配对
- 支持个人和群组
- 媒体消息完整支持

---

#### 快速配置

**步骤 1：运行配置命令**
```bash
openclaw channels connect whatsapp
```

**步骤 2：扫描二维码**
- 终端显示 QR 码
- 用手机 WhatsApp 扫描
- 等待配对成功

**步骤 3：配置访问控制**
```json
{
  "channels": {
    "whatsapp": {
      "allowFrom": ["+8613800138000"],
      "groups": {
        "*": { "requireMention": true }
      }
    }
  }
}
```

---

### Discord 配置

#### 创建 Discord 应用

1. 访问 https://discord.com/developers/applications
2. 点击 "New Application"
3. 输入应用名称
4. 进入 "Bot" 页面
5. 点击 "Add Bot"
6. 复制 Bot Token

---

#### 邀请 Bot 到服务器

1. 进入 "OAuth2" → "URL Generator"
2. 选择 scopes: `bot`
3. 选择权限：`Send Messages`, `Read Messages`
4. 复制生成的 URL
5. 在浏览器打开并选择服务器

---

#### 配置 OpenClaw

```json
{
  "channels": {
    "discord": {
      "botToken": "YOUR_BOT_TOKEN",
      "allowGuilds": ["123456789012345678"],
      "allowChannels": ["987654321098765432"]
    }
  }
}
```

---

### iMessage 配置（BlueBubbles）

#### 要求

- macOS 服务器（运行 BlueBubbles）
- BlueBubbles 应用安装
- REST API 访问权限

---

#### 安装 BlueBubbles

1. 访问 https://bluebubbles.app/
2. 下载 macOS 应用
3. 安装并启动
4. 完成设置（登录 Apple ID）
5. 启用 REST API

---

#### 配置 OpenClaw

```json
{
  "channels": {
    "bluebubbles": {
      "serverUrl": "http://your-mac:1234",
      "password": "your-password",
      "allowFrom": ["+8613800138000"]
    }
  }
}
```

---

### 飞书配置

#### 创建飞书机器人

1. 访问飞书开发者后台
2. 创建企业自建应用
3. 添加机器人能力
4. 获取 App ID 和 App Secret

---

#### 配置 OpenClaw

```json
{
  "channels": {
    "feishu": {
      "appId": "cli_xxxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxx",
      "allowUsers": ["ou_xxxxxxxxxxxxx"]
    }
  }
}
```

---

### Slack 配置

#### 创建 Slack 应用

1. 访问 https://api.slack.com/apps
2. 点击 "Create New App"
3. 选择工作区
4. 添加 Bot 用户
5. 获取 Bot Token

---

#### 配置 OpenClaw

```json
{
  "channels": {
    "slack": {
      "botToken": "xoxb-xxxxxxxxxxxx-xxxxxxxxxxxx-xxxxxxxxxxxx",
      "allowChannels": ["C0123456789"]
    }
  }
}
```

---

### 渠道路由规则

#### 基础路由

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

---

#### 高级路由

```json
{
  "routing": {
    "defaultAgent": "general-agent",
    "rules": [
      {
        "priority": 1,
        "channel": "telegram",
        "from": ["123456789"],
        "pattern": ".*紧急.*",
        "agent": "urgent-agent"
      },
      {
        "priority": 2,
        "channel": "*",
        "pattern": ".*帮助.*",
        "agent": "help-agent"
      }
    ]
  }
}
```

---

### 群组消息配置

#### Telegram 群组

```json
{
  "channels": {
    "telegram": {
      "groups": {
        "*": {
          "requireMention": true,
          "mentionPatterns": ["@bot", "@assistant"],
          "ignoreCommands": ["/start", "/help"]
        }
      }
    }
  }
}
```

---

#### Discord 频道

```json
{
  "channels": {
    "discord": {
      "guilds": {
        "*": {
          "requireMention": true,
          "allowedChannels": ["general", "bot-commands"]
        }
      }
    }
  }
}
```

---

## 第五部分：模型配置

### 模型选择指南

#### 按场景选择

| 场景 | 推荐模型 | 理由 |
|------|---------|------|
| **代码编程** | Claude Sonnet | 代码理解能力强 |
| **创意写作** | Claude Opus | 创意和表达能力强 |
| **快速响应** | GPT-4 Turbo | 速度快，成本低 |
| **多语言** | Gemini Pro | 多语言支持好 |
| **本地运行** | Ollama (Llama 3) | 无需 API，隐私好 |
| **性价比** | Claude Haiku | 便宜且快速 |

---

#### 模型性能对比

| 模型 | 速度 | 质量 | 成本 | 上下文 |
|------|------|------|------|--------|
| **Claude Sonnet** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | 200K |
| **Claude Opus** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐ | 200K |
| **Claude Haiku** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 200K |
| **GPT-4 Turbo** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | 128K |
| **GPT-4o** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | 128K |
| **Gemini Pro** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | 128K |

---

### 模型提供商目录

#### 国际提供商

| 提供商 | 模型 | 特点 | 官网 |
|--------|------|------|------|
| **Anthropic** | Claude | 代码能力强，安全 | https://anthropic.com |
| **OpenAI** | GPT | 通用能力强 | https://openai.com |
| **Google** | Gemini | 多模态 | https://deepmind.google |
| **xAI** | Grok | 实时数据 | https://x.ai |
| **Mistral** | Mistral | 开源模型 | https://mistral.ai |
| **Groq** | LPU | 超快速 | https://groq.com |

---

#### 中国提供商

| 提供商 | 模型 | 特点 | 官网 |
|--------|------|------|------|
| **阿里** | Qwen（通义千问） | 中文能力强 | https://tongyi.aliyun.com |
| **百度** | Qianfan（文心一言） | 中文优化 | https://cloud.baidu.com |
| **智谱** | GLM | 开源模型 | https://zhipu.ai |
| **月之暗面** | Moonshot（Kimi） | 长上下文 | https://moonshot.ai |
| **MiniMax** | MiniMax | 多模态 | https://minimaxi.com |
| **火山引擎** | Doubao（豆包） | 性价比高 | https://doubao.com |
| **Z.AI** | Zhipu | 开源生态 | https://z.ai |

---

#### 平台与网关

| 平台 | 支持模型 | 特点 |
|------|---------|------|
| **Amazon Bedrock** | 多厂商 | AWS 集成 |
| **Cloudflare AI Gateway** | 多厂商 | 边缘计算 |
| **OpenRouter** | 50+ 模型 | 统一 API |
| **LiteLLM** | 100+ 模型 | 开源代理 |
| **Vercel AI Gateway** | 多厂商 | Vercel 生态 |

---

#### 本地模型

| 平台 | 模型 | 要求 |
|------|------|------|
| **Ollama** | Llama 3, Mistral | 8GB+ RAM |
| **vLLM** | 多种模型 | GPU 推荐 |
| **SGLang** | 多种模型 | GPU 必须 |

---

### API Key 配置

#### 获取 API Key

**Anthropic**：
1. 访问 https://console.anthropic.com/
2. 注册/登录
3. 进入 "API Keys"
4. 点击 "Create Key"
5. 复制并安全保存

**OpenAI**：
1. 访问 https://platform.openai.com/api-keys
2. 登录
3. 点击 "Create new secret key"
4. 复制并安全保存

---

#### 配置方式

**方式 1：Onboarding 配置**
```bash
openclaw onboard
```

**方式 2：配置文件**
```json
{
  "models": {
    "providers": {
      "anthropic": {
        "apiKey": "sk-ant-xxx"
      },
      "openai": {
        "apiKey": "sk-xxx"
      }
    }
  }
}
```

**方式 3：环境变量**
```bash
export ANTHROPIC_API_KEY=sk-ant-xxx
export OPENAI_API_KEY=sk-xxx
```

---

### 模型故障转移

#### 配置故障转移

```json
{
  "models": {
    "default": "claude-sonnet-4-20250514",
    "failover": [
      "claude-sonnet-4-20250514",
      "gpt-4-turbo",
      "gemini-pro"
    ]
  }
}
```

---

#### 故障转移策略

1. **主模型失败** → 自动切换到备用模型 1
2. **备用 1 失败** → 自动切换到备用模型 2
3. **全部失败** → 返回错误消息

---

#### 监控故障

```bash
# 查看故障日志
openclaw logs | grep failover

# 查看当前模型
openclaw models list
```

---

### Token 使用与成本优化

#### Token 计算

- **输入 Token**：提示词长度
- **输出 Token**：回复长度
- **总计**：输入 + 输出

---

#### 成本对比（每 1K tokens）

| 模型 | 输入 | 输出 | 100 次对话成本* |
|------|------|------|---------------|
| **Claude Sonnet** | $0.003 | $0.015 | ~$0.18 |
| **Claude Haiku** | $0.00025 | $0.00125 | ~$0.015 |
| **GPT-4 Turbo** | $0.01 | $0.03 | ~$0.40 |
| **GPT-4o** | $0.005 | $0.015 | ~$0.20 |
| **Gemini Pro** | $0.0005 | $0.0015 | ~$0.02 |

*假设每次对话 1K 输入 + 1K 输出

---

#### 成本优化技巧

1. **使用提示词缓存**
   ```json
   {
     "models": {
       "cache": {
         "enabled": true,
         "maxSize": 1000
       }
     }
   }
   ```

2. **限制回复长度**
   ```json
   {
     "models": {
       "maxTokens": 1000
     }
   }
   ```

3. **选择合适的模型**
   - 简单任务：Haiku/Gemini
   - 复杂任务：Sonnet/GPT-4

4. **优化提示词**
   - 简洁明确
   - 避免冗余
   - 使用系统提示词

---

### 提示词缓存

#### 启用缓存

```json
{
  "models": {
    "cache": {
      "enabled": true,
      "maxSize": 2000,
      "ttl": 3600
    }
  }
}
```

---

#### 缓存效果

| 场景 | 无缓存 | 有缓存 | 节省 |
|------|--------|--------|------|
| **重复问题** | 全额计费 | 仅输出计费 | ~50% |
| **长上下文** | 全额计费 | 缓存部分免费 | ~70% |
| **系统提示词** | 每次计费 | 缓存后免费 | ~30% |

---

## 第六部分：配置参考

### 配置文件位置

| 系统 | 路径 |
|------|------|
| **macOS/Linux** | `~/.openclaw/openclaw.json` |
| **Windows** | `%USERPROFILE%\.openclaw\openclaw.json` |
| **Docker** | `/root/.openclaw/openclaw.json` |

---

### 配置键详解

#### 完整配置示例

```json
{
  "channels": {
    "telegram": {
      "botToken": "xxx",
      "allowFrom": ["123"],
      "allowGroups": ["-456"],
      "groups": {
        "*": {
          "requireMention": true
        }
      }
    }
  },
  "models": {
    "default": "claude-sonnet-4-20250514",
    "providers": {
      "anthropic": {
        "apiKey": "sk-ant-xxx"
      }
    },
    "failover": ["gpt-4-turbo"],
    "cache": {
      "enabled": true
    }
  },
  "routing": {
    "defaultAgent": "general-agent",
    "rules": []
  },
  "server": {
    "port": 18789,
    "host": "0.0.0.0"
  }
}
```

---

### 访问控制配置

#### 用户白名单

```json
{
  "channels": {
    "telegram": {
      "allowFrom": [
        "123456789",
        "987654321"
      ]
    }
  }
}
```

---

#### 群组白名单

```json
{
  "channels": {
    "telegram": {
      "allowGroups": [
        "-1001234567890",
        "-1009876543210"
      ]
    }
  }
}
```

---

#### IP 白名单

```json
{
  "server": {
    "allowIPs": [
      "192.168.1.0/24",
      "10.0.0.0/8"
    ]
  }
}
```

---

### 环境变量配置

| 变量 | 说明 | 默认值 | 示例 |
|------|------|--------|------|
| `OPENCLAW_PORT` | 服务端口 | 18789 | 18789 |
| `OPENCLAW_HOST` | 监听地址 | localhost | 0.0.0.0 |
| `OPENCLAW_LOG_LEVEL` | 日志级别 | info | debug |
| `ANTHROPIC_API_KEY` | Anthropic Key | - | sk-ant-xxx |
| `OPENAI_API_KEY` | OpenAI Key | - | sk-xxx |
| `OPENCLAW_CONFIG_DIR` | 配置目录 | ~/.openclaw | /etc/openclaw |

---

### 配置模板

#### 个人助理模板

```json
{
  "channels": {
    "telegram": {
      "botToken": "YOUR_BOT_TOKEN"
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

---

#### 团队协作文档

```json
{
  "channels": {
    "slack": {
      "botToken": "xoxb-xxx",
      "allowChannels": ["C0123456789"]
    }
  },
  "models": {
    "default": "claude-sonnet-4-20250514",
    "providers": {
      "anthropic": {
        "apiKey": "sk-ant-xxx"
      }
    }
  },
  "routing": {
    "rules": [
      {
        "pattern": ".*代码.*",
        "agent": "coding-agent"
      }
    ]
  }
}
```

---

## 第七部分：运维与监控

### 服务管理

#### systemd 管理

```bash
# 启动
sudo systemctl start openclaw

# 停止
sudo systemctl stop openclaw

# 重启
sudo systemctl restart openclaw

# 查看状态
sudo systemctl status openclaw

# 开机自启
sudo systemctl enable openclaw

# 禁用自启
sudo systemctl disable openclaw
```

---

#### macOS Launchd

```bash
# 加载服务
launchctl load ~/Library/LaunchAgents/com.openclaw.gateway.plist

# 卸载服务
launchctl unload ~/Library/LaunchAgents/com.openclaw.gateway.plist

# 启动
launchctl start com.openclaw.gateway

# 停止
launchctl stop com.openclaw.gateway
```

---

### 日志查看

#### 实时日志

```bash
openclaw logs
```

---

#### 日志级别

```json
{
  "logging": {
    "level": "info"
  }
}
```

| 级别 | 说明 | 使用场景 |
|------|------|---------|
| `debug` | 调试信息 | 开发调试 |
| `info` | 一般信息 | 生产环境 |
| `warn` | 警告信息 | 问题排查 |
| `error` | 错误信息 | 仅错误 |

---

#### 日志过滤

```bash
# 过滤错误
openclaw logs | grep ERROR

# 过滤特定渠道
openclaw logs | grep telegram

# 查看最近 100 行
openclaw logs --lines 100

# 导出日志
openclaw logs > openclaw.log
```

---

### 性能监控

#### 查看资源使用

```bash
# CPU 和内存
ps aux | grep openclaw

# 网络连接
netstat -tlnp | grep 18789

# 磁盘使用
du -sh ~/.openclaw
```

---

#### Dashboard 监控

打开 Dashboard：
```bash
openclaw dashboard
```

**监控指标**：
- 活跃会话数
- 消息处理量
- 平均响应时间
- 错误率

---

### 备份与恢复

#### 备份配置

```bash
# 备份配置文件
cp ~/.openclaw/openclaw.json ~/.openclaw/openclaw.json.bak

# 备份整个目录
tar -czf openclaw-backup-$(date +%Y%m%d).tar.gz ~/.openclaw
```

---

#### 恢复配置

```bash
# 恢复配置文件
cp ~/.openclaw/openclaw.json.bak ~/.openclaw/openclaw.json

# 恢复整个目录
tar -xzf openclaw-backup-20260322.tar.gz -C ~/
```

---

### 升级指南

#### 升级 OpenClaw

```bash
# 升级
npm install -g openclaw@latest

# 验证
openclaw --version

# 重启服务
openclaw restart
```

---

#### 回滚版本

```bash
# 安装指定版本
npm install -g openclaw@0.1.0

# 重启服务
openclaw restart
```

---

### 故障排查

#### 问题 1：端口被占用

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

---

#### 问题 2：API Key 无效

**错误**：`Invalid API key`

**解决**：
1. 检查 API Key 是否正确
2. 确认账户有额度
3. 重新运行 onboarding

---

#### 问题 3：渠道连接失败

**错误**：`Failed to connect to channel`

**解决**：
1. 检查网络连接
2. 验证渠道凭证
3. 查看日志：`openclaw logs`

---

#### 问题 4：模型不允许

**错误**：`Model is not allowed`

**解决**：
1. 检查模型名称
2. 验证提供商配置
3. 重新运行 onboarding

---

#### 问题 5：工具循环检测

**错误**：`Tool loop detected`

**解决**：
1. 检查工具调用逻辑
2. 增加最大迭代次数
3. 优化 Agent 提示词

---

## 第八部分：安全与生产

### 安全最佳实践

#### 1. API Key 保护

- ✅ 不提交到 Git
- ✅ 使用环境变量
- ✅ 定期轮换
- ✅ 创建专用 Key（非主账户）

---

#### 2. 访问控制

- ✅ 配置 `allowFrom` 白名单
- ✅ 群组要求 @提及
- ✅ IP 白名单
- ✅ 2FA 认证（如支持）

---

#### 3. 网络安全

- ✅ 使用 HTTPS（反向代理）
- ✅ 防火墙限制
- ✅ 内网部署
- ✅ VPN 访问

---

#### 4. 数据安全

- ✅ 加密存储
- ✅ 定期备份
- ✅ 日志脱敏
- ✅ 会话过期

---

### 生产环境部署

#### 系统要求

| 组件 | 要求 |
|------|------|
| **CPU** | 4 核心+ |
| **内存** | 8GB+ |
| **存储** | 20GB SSD |
| **网络** | 100Mbps |
| **系统** | Ubuntu 22.04 LTS |

---

#### 部署步骤

1. **安装依赖**
   ```bash
   sudo apt update
   sudo apt install -y nodejs npm nginx certbot
   ```

2. **安装 OpenClaw**
   ```bash
   npm install -g openclaw@latest
   ```

3. **配置系统服务**
   ```bash
   sudo systemctl enable openclaw
   sudo systemctl start openclaw
   ```

4. **配置 Nginx 反向代理**
   ```nginx
   server {
       listen 443 ssl;
       server_name ai.example.com;
       
       ssl_certificate /etc/letsencrypt/live/ai.example.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/ai.example.com/privkey.pem;
       
       location / {
           proxy_pass http://localhost:18789;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```

5. **配置防火墙**
   ```bash
   sudo ufw allow 443/tcp
   sudo ufw allow 22/tcp
   sudo ufw enable
   ```

---

### 高可用配置

#### 负载均衡

```nginx
upstream openclaw_backend {
    server 192.168.1.10:18789;
    server 192.168.1.11:18789;
    server 192.168.1.12:18789;
}

server {
    listen 443 ssl;
    
    location / {
        proxy_pass http://openclaw_backend;
    }
}
```

---

#### 会话同步

```json
{
  "session": {
    "store": "redis",
    "redis": {
      "url": "redis://192.168.1.20:6379"
    }
  }
}
```

---

### 数据隐私保护

#### 日志脱敏

```json
{
  "logging": {
    "redact": [
      "apiKey",
      "token",
      "password",
      "secret"
    ]
  }
}
```

---

#### 数据保留策略

```json
{
  "data": {
    "retention": {
      "sessions": 30,
      "logs": 7,
      "messages": 90
    }
  }
}
```

---

## 第九部分：开发与贡献

### 开发环境搭建

#### 克隆仓库

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
```

---

#### 安装依赖

```bash
npm install
```

---

#### 开发模式

```bash
# 开发模式运行
npm run dev

# 热重载
npm run watch
```

---

#### 运行测试

```bash
# 单元测试
npm test

# 集成测试
npm run test:integration

# 覆盖率
npm run test:coverage
```

---

### 插件开发

#### 创建插件

```bash
# 使用模板
npx @openclaw/create-plugin my-plugin

# 进入目录
cd my-plugin

# 安装依赖
npm install
```

---

#### 插件结构

```
my-plugin/
├── src/
│   ├── index.ts
│   ├── channel.ts
│   └── tools.ts
├── package.json
└── README.md
```

---

#### 发布插件

```bash
# 构建
npm run build

# 发布到 npm
npm publish
```

---

### 贡献指南

#### 提交代码

1. Fork 仓库
2. 创建分支：`git checkout -b feature/my-feature`
3. 提交更改：`git commit -am 'feat: add my feature'`
4. 推送分支：`git push origin feature/my-feature`
5. 创建 PR

---

#### 提交规范

```
feat: 新功能
fix: Bug 修复
docs: 文档更新
style: 代码格式
refactor: 重构
test: 测试
chore: 构建/工具
```

---

## 附录

### CLI 命令速查

#### 基础命令

```bash
openclaw start              # 启动服务
openclaw stop               # 停止服务
openclaw restart            # 重启服务
openclaw status             # 查看状态
openclaw logs               # 查看日志
openclaw dashboard          # 打开 Dashboard
```

---

#### Onboarding

```bash
openclaw onboard            # 运行配置向导
openclaw onboard --reset    # 重置配置
```

---

#### 模型

```bash
openclaw models list        # 列出模型
openclaw models set <name>  # 设置模型
openclaw models test        # 测试模型
```

---

#### 渠道

```bash
openclaw channels list      # 列出渠道
openclaw channels connect <channel>  # 连接渠道
openclaw channels disconnect <channel>  # 断开渠道
```

---

#### 配置

```bash
openclaw config check       # 检查配置
openclaw config export      # 导出配置
openclaw config import      # 导入配置
openclaw config reset       # 重置配置
```

---

### 常见问题 FAQ

#### Q: OpenClaw 是免费的吗？

**A**: OpenClaw 本身是免费开源的（MIT 许可证），但需要支付模型提供商的 API 费用。

---

#### Q: 需要自己的服务器吗？

**A**: 是的，OpenClaw 是自托管方案，需要有自己的服务器或本地电脑运行。

---

#### Q: 支持哪些聊天应用？

**A**: 支持 30+ 聊天应用，包括 Telegram、WhatsApp、Discord、iMessage、飞书、Slack 等。

---

#### Q: 数据会上传到 OpenClaw 服务器吗？

**A**: 不会。所有数据都在你的服务器本地处理和存储。

---

#### Q: 可以同时连接多个渠道吗？

**A**: 可以，支持同时连接多个渠道，消息会路由到同一个 Agent。

---

#### Q: 如何备份数据？

**A**: 备份 `~/.openclaw` 目录即可，包含所有配置和会话数据。

---

#### Q: 支持中文吗？

**A**: 支持，取决于选择的模型。推荐使用 Claude 或 GPT-4，中文能力优秀。

---

#### Q: 可以离线运行吗？

**A**: 可以，使用 Ollama 等本地模型可完全离线运行。

---

### 资源链接

#### 官方资源

- **官网**: https://openclaw.ai/
- **文档**: https://docs.openclaw.ai/
- **GitHub**: https://github.com/openclaw/openclaw
- **Discord**: https://discord.com/invite/clawd
- **Releases**: https://github.com/openclaw/openclaw/releases

#### 社区资源

- **Discord 社区**: 用户论坛和技术支持
- **GitHub Issues**: Bug 报告和功能请求
- **插件市场**: （即将推出）

---

## 许可证

**MIT License**

Copyright (c) 2026 OpenClaw

允许免费使用、复制、修改、合并、出版、发行、再授权。

详见 [LICENSE](https://github.com/openclaw/openclaw/blob/main/LICENSE)

---

## 致谢

感谢所有贡献者和社区成员！

**"EXFOLIATE! EXFOLIATE!"** — A space lobster, probably

---

**文档版本**: v3.0 完整版  
**最后更新**: 2026-03-23  
**内容来源**: 基于官方文档 https://docs.openclaw.ai/ 深度优化  
**优化内容**: 9 大部分 52 章节，覆盖新手入门到生产级部署  
**GitHub 推送**: 待推送
