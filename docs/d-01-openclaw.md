# 🦞 OpenClaw 龙虾机器人完全指南

> **最新修改**: 2026-03-22  
> **官方文档**: https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **Discord**: https://discord.com/invite/clawd

---

## 📑 目录

### 第 0 部分 快速开始
- [0.1 什么是 OpenClaw](#01-什么是-openclaw)
- [0.2 核心特性](#02-核心特性)
- [0.3 快速安装](#03-快速安装)

### 第 1 部分 AI 编程基础
- [1.1 AI 编程产品分类](#11-ai-编程产品分类)
- [1.2 AI 编程主流模型](#12-ai-编程主流模型)
- [1.3 AI 编程必知术语](#13-ai-编程必知术语)

### 第 2 部分 核心定位
- [2.1 解决什么问题](#21-解决什么问题)
- [2.2 不做什么](#22-不做什么)
- [2.3 设计理念](#23-设计理念)

### 第 3 部分 功能特性
- [3.1 核心功能](#31-核心功能)
- [3.2 扩展功能](#32-扩展功能)

### 第 4 部分 架构组成
- [4.1 整体架构](#41-整体架构)
- [4.2 核心组件](#42-核心组件)

### 第 5 部分 部署方式
- [5.1 部署方式对比](#51-部署方式对比)
- [5.2 系统要求](#52-系统要求)

### 第 6 部分 本地部署教程
- [6.1 环境准备](#61-环境准备)
- [6.2 安装 OpenClaw](#62-安装-openclaw)
- [6.3 配置 OpenClaw](#63-配置-openclaw)
- [6.4 启动 OpenClaw](#64-启动-openclaw)

### 第 7 部分 云端部署教程
- [7.1 选择云服务商](#71-选择云服务商)
- [7.2 云服务器配置](#72-云服务器配置)
- [7.3 部署步骤](#73-部署步骤)
- [7.4 域名与 HTTPS](#74-域名与-https)

### 第 8 部分 渠道配置
- [8.1 支持的聊天渠道](#81-支持的聊天渠道)
- [8.2 飞书渠道配置](#82-飞书渠道配置)
- [8.3 钉钉渠道配置](#83-钉钉渠道配置)
- [8.4 企业微信渠道配置](#84-企业微信渠道配置)
- [8.5 电报渠道配置](#85-电报渠道配置)
- [8.6 QQ 渠道配置](#86-qq 渠道配置)

### 第 9 部分 模型配置
- [9.1 支持的大模型](#91-支持的大模型)
- [9.2 OpenAI GPT 配置](#92-openai-gpt 配置)
- [9.3 Anthropic Claude 配置](#93-anthropic-claude 配置)
- [9.4 Google Gemini 配置](#94-google-gemini 配置)
- [9.5 阿里通义千问配置](#95-阿里通义千问配置)
- [9.6 百度文心一言配置](#96-百度文心一言配置)
- [9.7 模型选择建议](#97-模型选择建议)

### 第 10 部分 联网搜索配置
- [10.1 支持的搜索引擎](#101-支持的搜索引擎)
- [10.2 Google Custom Search 配置](#102-google-custom-search 配置)
- [10.3 Bing Search 配置](#103-bing-search 配置)
- [10.4 Tavily Search 配置](#104-tavily-search 配置)

### 第 11 部分 配置文件详解
- [11.1 完整配置示例](#111-完整配置示例)
- [11.2 环境变量配置](#112-环境变量配置)
- [11.3 配置优先级](#113-配置优先级)

### 第 12 部分 常见问题
- [12.1 安装问题](#121-安装问题)
- [12.2 配置问题](#122-配置问题)
- [12.3 渠道问题](#123-渠道问题)
- [12.4 模型问题](#124-模型问题)
- [12.5 性能问题](#125-性能问题)

### 附录
- [附录 A: 37 个章节完整目录](#附录-a-37-个章节完整目录)
- [附录 B: 核心概念详解](#附录-b-核心概念详解)
- [附录 C: Skills vs MCP 关系图](#附录-c-skills-vs-mcp 关系图)

---

## 第 0 部分 快速开始

### 0.1 什么是 OpenClaw

**OpenClaw（龙虾机器人）** 是一款开源的 AI 自动化助手，旨在简化内容创作与运营中的机械性工作。

**核心定位**: 基于大模型的自动化工具，帮你完成重复性工作

**官方网站**: 
- 文档：https://docs.openclaw.ai/
- GitHub: https://github.com/openclaw/openclaw
- Discord: https://discord.com/invite/clawd

**开源协议**: MIT License（免费开源）

**大模型费用**: 使用大模型服务需要付费（按 Token 计费）

### 0.2 核心特性

| 特性 | 说明 | 优势 |
|------|------|------|
| **多渠道支持** | 飞书、钉钉、企业微信、Telegram、QQ | 随时随地访问 |
| **多模型支持** | GPT-4、Claude、Gemini、通义千问、文心一言 | 灵活选择，成本可控 |
| **Skills 系统** | 可扩展的技能插件 | 自定义功能，无限可能 |
| **MCP 协议** | 模型上下文协议 | 连接外部工具，突破局限 |
| **联网搜索** | Google、Bing、Tavily | 实时获取最新信息 |
| **定时任务** | Cron 表达式配置 | 自动化执行计划任务 |
| **本地部署** | 完全控制，数据私密 | 安全可靠，免费使用 |

### 0.3 快速安装

#### 方式一：npm 安装（推荐）

```bash
# 安装 Node.js (v18+)
# https://nodejs.org/

# 全局安装 OpenClaw
npm install -g @openclaw/core

# 验证安装
openclaw --version

# 初始化配置
openclaw init

# 启动服务
openclaw start
```

#### 方式二：Docker 安装

```bash
# 拉取镜像
docker pull openclaw/core:latest

# 运行容器
docker run -d \
  --name openclaw \
  -p 3000:3000 \
  -v ./config:/app/config \
  -v ./data:/app/data \
  openclaw/core:latest
```

#### 方式三：源码安装

```bash
# 克隆仓库
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 编译构建
npm run build

# 启动服务
npm start
```

### 0.4 适用人群

| 用户类型 | 核心价值 | 典型场景 |
|---------|---------|---------|
| **普通人** | 零门槛私人数字管家 | 日常任务管理、信息查询、日程安排 |
| **IT 从业者** | 技术流程效率工具 | 代码生成、自动化脚本、技术文档 |
| **企业用户** | 轻量化办公自动化助手 | 工作流程自动化、数据报表、客服响应 |
| **自媒体** | 内容运营提速工具 | 选题素材、内容排版、运营分发、数据复盘 |
| **开发者** | 可扩展的 AI 平台 | Skills 开发、插件定制、二次开发 |

---

## 第 1 部分 AI 编程基础

### 0.1 AI 编程产品分类

| 大类分类 | 核心工具 | 核心特点 | 适用场景 |
|---------|---------|---------|---------|
| **Chat 聊天型** | OpenAI: ChatGPT<br>Anthropic: Claude<br>Google: Gemini | 自然语言对话<br>无专属编程环境<br>轻量化问答<br>零门槛 | 代码咨询<br>片段生成<br>Bug 排查<br>思路梳理 |
| **IDE 集成型** | Kiro<br>Cursor<br>Antigravity | 原生 AI IDE<br>沉浸式编码<br>实时补全、调试<br>项目级辅助 | 专业项目开发<br>日常编码<br>全栈工程编写 |
| **CLI 命令行型** | OpenAI：Codex<br>Anthropic：Claude Code | 纯终端交互<br>无图形界面<br>高效批量处理<br>自动化运维 | 服务器开发<br>命令行批量操作<br>自动化部署 |

### 0.2 AI 编程主流模型

#### 国际 AI 编程工具最新模型

| 厂商 | 系列 | 模型 |
|------|------|------|
| **OpenAI** | ChatGPT、Codex | GPT-5.4<br>GPT-5.3-Codex |
| **Anthropic** | ClaudeCode | Claude Opus 4.6<br>Claude Sonnet 4.6 |
| **Google** | Gemini | Gemini 3.1 Pro<br>大香蕉 |

#### 国内 AI 编程工具最新模型

| 厂商 | 系列 | 模型 |
|------|------|------|
| **阿里** | 通义千问 Qwen | Qwen 2.5 Code |

### 0.3 AI 编程必知术语

#### 3.1 AI 大模型

**定义**: 基于深度学习的人工智能模型，能够理解和生成人类语言

**特点**:
- 海量训练数据
- 强大的语言理解能力
- 多任务处理能力

#### 3.2 Token

**定义**: AI 大模型处理文本的基本计量单位

**换算关系**:
- 英文：1 Token ≈ 4 个字符 ≈ 0.75 个单词
- 中文：1 Token ≈ 1.5 个汉字

**计费方式**: 按 Token 数量计费（输入 + 输出）

#### 3.3 提示词（Prompt）

**定义**: 发给 AI 大模型的精准编程指令，是 AI 编程里最核心的操作

**编写原则**:
- ✅ 不能太笼统，越具体越好用
- ✅ 完整清晰的需求就是标准提示词
- ✅ 指令越明确，AI 给出的代码结果越精准

**优秀示例**:
```
帮我排查这段 Java 代码的空指针异常，保留原有业务逻辑，逐行添加易懂的中文注释
```

**好处**: 省去反复修改的麻烦

**编写公式**: 具体任务 + 约束条件 + 输出要求

#### 3.4 上下文长度（Context Length）

**定义**: AI 大模型的短期记忆力上限，计量单位是 Token，代表模型能一次性完整记住、连贯处理的所有前置内容总量

**编程场景应用**:
- 粘贴一整段长代码让 AI 逐行分析优化
- 多轮对话的连续编程需求

**问题**: 上下文长度太短 → AI 会"断片儿"，只能处理后半段

**优势**: 上下文长度越长 → AI 越能承接整段长代码，全程逻辑连贯不脱节

**优化建议**:
- 分段提交长代码
- 关键信息前置
- 重要逻辑重复强调

#### 3.5 Skills（技能）

**定义**: Skills 是给 AI 大模型定制的专项能力插件包，是 AI 完成精准编程任务的核心专属技能，并非模型自带的泛化能力，而是针对性配置的专业功能模块

**常见 Skills 类型**:
| Skill 类型 | 功能说明 |
|-----------|---------|
| **代码生成 Skill** | 根据需求自动生成代码 |
| **Bug 排查修复 Skill** | 定位并修复代码错误 |
| **SQL 语句编写 Skill** | 生成和优化 SQL 查询 |
| **接口调试 Skill** | API 接口测试和调试 |
| **代码注释生成 Skill** | 自动添加代码注释 |

**工作原理**:
1. AI 接到编程需求
2. 自动匹配并调用对应的 Skills
3. 依靠专项技能高效完成任务

**优势**:
- ✅ 提升结果专业性
- ✅ 避免输出偏离需求
- ✅ 相当于给 AI 装上了细分的编程专业工具箱
- ✅ 想用哪项功能就调用对应技能

#### 3.6 MCP（模型上下文协议）

**全称**: Model Context Protocol（模型上下文协议）

**定义**: 是 AI 编程与大模型应用里的通用连接标准，可以通俗理解为 AI 世界的"USB-C 统一接口"

**解决的痛点**:
- ❌ **MCP 出现前**: 让 AI 连接数据库、代码仓库、本地文件、编程调试工具，需要单独写适配代码，换一个大模型就要重新适配
- ✅ **MCP 出现后**: 不管是 GPT 还是 Claude 这类编程大模型，都能通过标准化方式无缝对接各类外部资源，不用重复开发适配逻辑

**与 Skills 的关系**:
| 组件 | 职责 | 比喻 |
|------|------|------|
| **MCP** | 负责打通 AI 和外部工具的连接通道 | USB-C 接口 |
| **Skills** | AI 通过这个通道调用工具后，执行具体任务的专项能力 | 插在 USB-C 上的设备功能 |

**配合效果**:
1. MCP 打通连接通道
2. Skills 执行具体任务
3. AI 突破自身局限，调用外部资源
4. 完成更复杂的编程任务

**典型应用场景**:
- 直接读取本地项目代码
- 连接数据库查数据
- 调用接口调试
- 大幅提升 AI 编程的实用性

---

## 1. OpenClaw 概述

### 1.1 什么是 OpenClaw

**OpenClaw（龙虾机器人）** 是一款开源的 AI 自动化助手，旨在简化内容创作与运营中的机械性工作。

**官方网址**: https://docs.openclaw.ai/zh-CN

**核心定位**: 简化创作与运营机械工作

### 1.2 龙虾的由来

**品牌演变历史**:

| 阶段 | 名称 | 原因 |
|------|------|------|
| **最初** | Clawdbot | 原始名称 |
| **第一次改名** | Moltbot | 因为 Clawd 的发音和 A 社的 Claude 发音很相似（都叫克劳德），被 A 社盯上，避免版权纠纷 |
| **最终名称** | OpenClaw | 仅过了三天又改名 |

**品牌寓意**:
- **Claw** = 爪子或者龙虾的鳌 🦞
- **选择龙虾的原因**: 作者的家乡盛产龙虾，算是给家乡代言了

### 1.3 为什么这么火

**市场痛点分析**:

| AI 产品类型 | 代表产品 | 优势 | 劣势 |
|------------|---------|------|------|
| **网页聊天 AI** | DeepSeek、豆包、千问 | 随时随地访问 | ❌ 无法访问和管理本地文件<br>❌ 无法安装软件<br>❌ 与电脑环境隔离 |
| **编程 AI 助手** | ClaudeCode、Codex | 可以接管电脑环境<br>可以安装软件 | ❌ 必须在电脑面前对话<br>❌ 离开电脑就指挥不了 |

**核心痛点**: 
> 聊天 AI 无法接管电脑环境，编程 AI 能接管电脑环境，但是无法随时随地使用。
> 这就造成了一种**鱼和熊掌不可兼得**的场面。

**龙虾机器人的解决方案**:
> 解决了无法随时随地在任意地方指挥家里的 AI 干活的痛点。

**商机洞察**:
- 随时随地
- 任意地方
- 指挥家里的 AI 干活

### 1.4 开源协议

- **许可证**: MIT License
- **费用**: OpenClaw 本身免费开源
- **大模型**: 使用大模型服务需要付费（按 Token 计费）

### 1.5 适用人群

| 用户类型 | 核心价值 | 典型场景 |
|---------|---------|---------|
| **普通人** | 零门槛私人数字管家 | 日常任务管理、信息查询、日程安排 |
| **IT 从业者** | 技术流程效率工具 | 代码生成、自动化脚本、技术文档 |
| **企业用户** | 轻量化办公自动化助手 | 工作流程自动化、数据报表、客服响应 |
| **自媒体** | 内容运营提速工具 | 选题素材、内容排版、运营分发、数据复盘 |

---

## 2. 核心定位

### 2.1 解决什么问题

OpenClaw 专注于解决内容创作与运营中的**机械性重复工作**：

- ✅ 自动收集选题素材
- ✅ 智能内容排版
- ✅ 多平台运营分发
- ✅ 数据自动复盘

### 2.2 不做什么

- ❌ 不替代人类创意
- ❌ 不做决策判断
- ❌ 不处理复杂逻辑

### 2.3 设计理念

**简单、高效、可扩展**

- 开箱即用，无需复杂配置
- 模块化设计，支持自定义扩展
- 支持多种聊天渠道接入
- 支持多种大模型对接

---

## 3. 功能特性

### 3.1 核心功能

| 功能模块 | 描述 | 适用场景 |
|---------|------|---------|
| **选题素材** | 自动收集热点、关键词、竞品分析 | 内容策划、市场调研 |
| **内容排版** | 自动格式化、美化、适配多平台 | 公众号、知乎、小红书 |
| **运营分发** | 一键发布到多个平台 | 多平台同步运营 |
| **数据复盘** | 自动收集阅读、点赞、评论数据 | 效果分析、优化策略 |

### 3.2 扩展功能

- **Skills 系统**: 支持自定义技能扩展
- **MCP 协议**: 模型上下文协议，支持复杂对话
- **联网搜索**: 实时获取最新信息
- **定时任务**: 自动化执行计划任务

---

## 4. 架构组成

### 4.1 整体架构

```
┌─────────────────────────────────────────────────┐
│              用户交互层（聊天渠道）               │
│   飞书 │ 钉钉 │ 企业微信 │ 电报 │ QQ │ 微信     │
└─────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────┐
│              OpenClaw 核心引擎                    │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐      │
│  │ 消息处理 │  │ 技能管理 │  │ 上下文管理│      │
│  └──────────┘  └──────────┘  └──────────┘      │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐      │
│  │ 配置管理 │  │ 日志系统 │  │ 定时任务 │      │
│  └──────────┘  └──────────┘  └──────────┘      │
└─────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────┐
│              大模型服务层                         │
│  GPT-4 │ Claude │ Gemini │ 通义千问 │ 文心一言  │
└─────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────┐
│              外部服务层                           │
│  联网搜索 │ 数据库 │ API 接口 │ 文件存储        │
└─────────────────────────────────────────────────┘
```

### 4.2 核心组件

| 组件 | 说明 | 作用 |
|------|------|------|
| **Core** | 核心引擎 | 消息路由、技能调度、上下文管理 |
| **Skills** | 技能系统 | 扩展功能模块，支持自定义 |
| **Channels** | 渠道适配器 | 对接飞书、钉钉、企业微信等 |
| **Models** | 模型适配器 | 对接 GPT、Claude、Gemini 等 |
| **Config** | 配置管理 | YAML 配置文件解析 |
| **Logger** | 日志系统 | 运行日志记录与查询 |

---

## 第 5 部分 部署方式

### 5.1 部署方式对比

| 部署方式 | 优点 | 缺点 | 适用场景 | 推荐指数 |
|---------|------|------|---------|---------|
| **npm 安装** | 官方推荐、更新及时、跨平台 | 需要 Node.js 环境 | ⭐⭐⭐⭐⭐ 强烈推荐 |
| **Docker 部署** | 环境隔离、一键部署、易迁移 | 需要 Docker 基础 | ⭐⭐⭐⭐⭐ 强烈推荐 |
| **源码安装** | 完全控制、可定制、最新代码 | 需要编译构建 | ⭐⭐⭐⭐ 开发者推荐 |
| **本地部署** | 数据私密、完全控制、免费 | 需要服务器资源、自行维护 | ⭐⭐⭐ 个人使用 |
| **云端部署** | 免维护、高可用、弹性扩展 | 需要付费、数据在云端 | ⭐⭐⭐⭐ 企业用户 |

### 5.2 系统要求

**最低配置**:
- CPU: 2 核
- 内存：4GB
- 磁盘：20GB
- 系统：Linux/macOS/Windows
- Node.js: v18+ (npm 安装)
- 或 Docker: 20.10+ (Docker 安装)

**推荐配置**:
- CPU: 4 核+
- 内存：8GB+
- 磁盘：50GB+
- 系统：Ubuntu 20.04+/CentOS 8+/macOS 12+
- Node.js: v20 LTS
- Docker: 最新版

---

## 第 6 部分 本地部署教程

### 6.1 环境准备

#### 6.1.1 安装 Node.js

**方式一：使用官方安装包**

访问 https://nodejs.org/ 下载并安装 LTS 版本（推荐 v20）

**方式二：使用包管理器**

```bash
# Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# CentOS/RHEL
curl -fsSL https://rpm.nodesource.com/setup_20.x | sudo bash -
sudo yum install -y nodejs

# macOS (Homebrew)
brew install node@20

# Windows
# 下载安装包：https://nodejs.org/
```

#### 6.1.2 验证安装

```bash
# 检查 Node.js 版本
node --version
# 应显示：v20.x.x

# 检查 npm 版本
npm --version
# 应显示：10.x.x
```

### 6.2 安装 OpenClaw

#### 6.2.1 全局安装（推荐）

```bash
# 全局安装 OpenClaw
npm install -g @openclaw/core

# 验证安装
openclaw --version

# 查看帮助
openclaw --help
```

#### 6.2.2 本地安装（开发用）

```bash
# 创建项目目录
mkdir my-openclaw
cd my-openclaw

# 初始化 npm 项目
npm init -y

# 安装 OpenClaw
npm install @openclaw/core

# 添加到 package.json
npm install --save @openclaw/core
```

#### 6.2.3 Docker 安装

```bash
# 拉取最新镜像
docker pull openclaw/core:latest

# 运行容器
docker run -d \
  --name openclaw \
  -p 3000:3000 \
  -v $(pwd)/config:/app/config \
  -v $(pwd)/data:/app/data \
  -e OPENCLAW_MODEL_API_KEY=your-api-key \
  openclaw/core:latest

# 查看日志
docker logs -f openclaw

# 停止容器
docker stop openclaw

# 启动容器
docker start openclaw
```

#### 6.2.4 源码安装

```bash
# 克隆仓库
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 编译构建
npm run build

# 测试运行
npm test

# 启动服务
npm start
```

### 6.3 配置 OpenClaw

#### 6.3.1 初始化配置

```bash
# 初始化配置（交互式）
openclaw init

# 或手动创建配置文件
mkdir -p ~/.openclaw
vim ~/.openclaw/config.yaml
```

#### 6.3.2 配置文件示例

```yaml
# ~/.openclaw/config.yaml

# 应用配置
app:
  name: "OpenClaw"
  version: "1.0.0"
  debug: false
  log_level: "INFO"

# 模型配置
model:
  provider: "openai"  # 或 claude/gemini/qwen/wenxin
  api_key: "sk-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "gpt-4"
  temperature: 0.7
  max_tokens: 2048

# 渠道配置
channel:
  # 飞书
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    verification_token: "xxxxxxxxxxxxxxxxxxxxxxxx"
  
  # 钉钉
  dingtalk:
    enabled: false
    app_key: "xxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
  
  # Telegram
  telegram:
    enabled: false
    bot_token: "xxxxxxxxx:xxxxxxxxxxxxxxxxxxxxxxxxxxx"

# 搜索配置
search:
  enabled: true
  provider: "google"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  search_engine_id: "xxxxxxxxxxxxx"

# 数据库配置
database:
  type: "sqlite"
  path: "~/.openclaw/data/openclaw.db"

# 定时任务
scheduler:
  enabled: true
  timezone: "Asia/Shanghai"
```

#### 6.3.3 使用环境变量

```bash
# .env 文件
OPENCLAW_MODEL_PROVIDER=openai
OPENCLAW_MODEL_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx
OPENCLAW_MODEL_MODEL_NAME=gpt-4
OPENCLAW_CHANNEL_FEISHU_APP_ID=cli_xxxxxxxxxxxxx
OPENCLAW_CHANNEL_FEISHU_APP_SECRET=xxxxxxxxxxxxxxxxxxxxxxxx
```

### 6.4 启动 OpenClaw

#### 6.4.1 命令行启动

```bash
# 启动服务
openclaw start

# 前台运行（查看日志）
openclaw run

# 指定配置文件
openclaw start --config /path/to/config.yaml

# 测试配置
openclaw test
```

#### 6.4.2 后台运行

```bash
# 使用 nohup 后台运行
nohup openclaw run > openclaw.log 2>&1 &

# 查看日志
tail -f openclaw.log

# 查看进程
ps aux | grep openclaw

# 停止服务
pkill -f openclaw
```

#### 6.4.3 使用 systemd 管理（Linux 推荐）

```bash
# 创建 systemd 服务文件
sudo vim /etc/systemd/system/openclaw.service
```

**服务文件内容**:
```ini
[Unit]
Description=OpenClaw AI Assistant
After=network.target

[Service]
Type=simple
User=your-user
WorkingDirectory=/home/your-user
Environment="PATH=/usr/bin"
Environment="OPENCLAW_CONFIG=/home/your-user/.openclaw/config.yaml"
ExecStart=/usr/bin/openclaw run
Restart=always
RestartSec=10
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

**启动服务**:
```bash
# 重载 systemd
sudo systemctl daemon-reload

# 启用服务
sudo systemctl enable openclaw

# 启动服务
sudo systemctl start openclaw

# 查看状态
sudo systemctl status openclaw

# 查看日志
sudo journalctl -u openclaw -f

# 重启服务
sudo systemctl restart openclaw

# 停止服务
sudo systemctl stop openclaw
```

#### 6.4.4 Docker 运行

```bash
# 使用 docker-compose（推荐）
cat > docker-compose.yml <<EOF
version: '3.8'
services:
  openclaw:
    image: openclaw/core:latest
    container_name: openclaw
    restart: always
    ports:
      - "3000:3000"
    volumes:
      - ./config:/app/config
      - ./data:/app/data
    environment:
      - OPENCLAW_MODEL_API_KEY=your-api-key
      - OPENCLAW_MODEL_PROVIDER=openai
EOF

# 启动服务
docker-compose up -d

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down
```

#### 6.4.5 验证运行

```bash
# 检查服务状态
curl http://localhost:3000/health

# 应返回
# {"status": "ok", "version": "1.0.0"}
```

---

## 7. 云端部署教程

### 7.1 选择云服务商

| 云服务商 | 优点 | 缺点 | 推荐指数 |
|---------|------|------|---------|
| **阿里云** | 国内访问快、生态完善 | 价格中等 | ⭐⭐⭐⭐ |
| **腾讯云** | 性价比高、服务好 | 生态略逊 | ⭐⭐⭐⭐ |
| **华为云** | 安全可靠、政企首选 | 价格略高 | ⭐⭐⭐ |
| **AWS** | 全球覆盖、功能强大 | 国内访问慢 | ⭐⭐⭐ |

### 7.2 云服务器配置

**推荐配置**（适合中小企业）:
- 实例：2 核 4G
- 系统：Ubuntu 20.04 LTS
- 带宽：3-5Mbps
- 存储：50GB SSD

**预估费用**:
- 阿里云：约 ¥200-300/月
- 腾讯云：约 ¥180-280/月
- 华为云：约 ¥220-320/月

### 7.3 部署步骤

#### 7.3.1 购买云服务器

1. 注册云服务商账号
2. 实名认证
3. 选择配置并购买
4. 设置 root 密码

#### 7.3.2 连接服务器

```bash
# SSH 连接
ssh root@your-server-ip

# 输入密码登录
```

#### 7.3.3 安装环境

```bash
# 更新系统
sudo apt update && sudo apt upgrade -y

# 安装 Python 和 Git
sudo apt install -y python3 python3-pip python3-venv git

# 安装防火墙
sudo apt install -y ufw
sudo ufw allow 22/tcp
sudo ufw enable
```

#### 7.3.4 部署 OpenClaw

参考 [6.2 安装 OpenClaw](#62-安装-openclaw) 步骤

### 7.4 域名与 HTTPS

#### 7.4.1 绑定域名

1. 在云服务商控制台绑定域名
2. 配置 DNS 解析（A 记录指向服务器 IP）
3. 等待 DNS 生效（通常 10 分钟）

#### 7.4.2 配置 HTTPS

```bash
# 安装 Certbot
sudo apt install -y certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d your-domain.com

# 自动续期
sudo certbot renew --dry-run
```

---

## 8. 渠道配置

### 8.1 支持的聊天渠道

| 渠道 | 状态 | 配置难度 | 适用场景 |
|------|------|---------|---------|
| **飞书** | ✅ 已支持 | ⭐⭐ | 企业办公 |
| **钉钉** | ✅ 已支持 | ⭐⭐ | 企业办公 |
| **企业微信** | ✅ 已支持 | ⭐⭐⭐ | 企业办公 |
| **电报 (Telegram)** | ✅ 已支持 | ⭐ | 个人使用 |
| **QQ** | ✅ 已支持 | ⭐⭐⭐ | 个人使用 |
| **微信** | ⚠️ 有限支持 | ⭐⭐⭐⭐ | 个人使用 |

### 8.2 飞书渠道配置

#### 8.2.1 创建飞书应用

1. 访问 [飞书开放平台](https://open.feishu.cn/)
2. 登录飞书账号
3. 点击"创建应用"
4. 填写应用信息（名称、图标、描述）
5. 获取 `App ID` 和 `App Secret`

#### 8.2.2 配置机器人

1. 进入应用管理后台
2. 添加"机器人"功能
3. 获取 `Verification Token`
4. 配置事件订阅（接收消息）
5. 配置权限（发送消息、读取消息等）

#### 8.2.3 发布应用

1. 提交应用审核
2. 审核通过后发布
3. 将机器人添加到群聊

#### 8.2.4 配置文件

```yaml
# config.yaml
channel:
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    verification_token: "xxxxxxxxxxxxxxxxxxxxxxxx"
```

### 8.3 钉钉渠道配置

#### 8.3.1 创建钉钉应用

1. 访问 [钉钉开放平台](https://open.dingtalk.com/)
2. 登录钉钉账号
3. 创建企业内部应用
4. 获取 `AppKey` 和 `AppSecret`

#### 8.3.2 配置机器人

1. 添加"机器人"功能
2. 获取 `Webhook` 地址
3. 配置安全设置（加签密钥）

#### 8.3.3 配置文件

```yaml
channel:
  dingtalk:
    enabled: true
    app_key: "xxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    webhook: "https://oapi.dingtalk.com/robot/send?access_token=xxx"
    secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
```

### 8.4 企业微信渠道配置

#### 8.4.1 创建企业微信应用

1. 访问 [企业微信管理后台](https://work.weixin.qq.com/)
2. 登录企业微信
3. 创建自建应用
4. 获取 `CorpID`、`AgentID`、`Secret`

#### 8.4.2 配置文件

```yaml
channel:
  wecom:
    enabled: true
    corp_id: "wwxxxxxxxxxxxx"
    agent_id: 1000001
    secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    token: "xxxxxxxxxxxxxxxx"
    encoding_aes_key: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### 8.5 电报（Telegram）渠道配置

#### 8.5.1 创建 Telegram 机器人

1. 在 Telegram 搜索 `@BotFather`
2. 发送 `/newbot` 创建机器人
3. 设置机器人名称和用户名
4. 获取 `Bot Token`

#### 8.5.2 配置文件

```yaml
channel:
  telegram:
    enabled: true
    bot_token: "xxxxxxxxx:xxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### 8.6 QQ 渠道配置

#### 8.6.1 使用 OneBot 协议

1. 安装 OneBot 适配器（如 go-cqhttp）
2. 配置 QQ 账号登录
3. 获取 WebSocket 连接地址

#### 8.6.2 配置文件

```yaml
channel:
  qq:
    enabled: true
    protocol: "onebot"
    ws_url: "ws://127.0.0.1:8080/ws"
    access_token: "your-token"
```

---

## 9. 模型配置

### 9.1 支持的大模型

| 厂商 | 模型 | 状态 | 配置难度 |
|------|------|------|---------|
| **OpenAI** | GPT-4/GPT-3.5 | ✅ 已支持 | ⭐ |
| **Anthropic** | Claude 3/2 | ✅ 已支持 | ⭐ |
| **Google** | Gemini Pro | ✅ 已支持 | ⭐⭐ |
| **阿里** | 通义千问 Qwen | ✅ 已支持 | ⭐⭐ |
| **百度** | 文心一言 | ✅ 已支持 | ⭐⭐ |
| **腾讯** | 混元大模型 | ✅ 已支持 | ⭐⭐ |
| **智谱** | ChatGLM | ✅ 已支持 | ⭐⭐ |

### 9.2 OpenAI GPT 配置

#### 9.2.1 获取 API Key

1. 访问 [OpenAI 平台](https://platform.openai.com/)
2. 注册/登录账号
3. 进入 API Keys 页面
4. 创建新的 API Key

#### 9.2.2 配置文件

```yaml
model:
  provider: "openai"
  api_key: "sk-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "gpt-4"  # 或 gpt-3.5-turbo
  base_url: "https://api.openai.com/v1"  # 可选，使用代理时配置
  temperature: 0.7
  max_tokens: 2048
```

### 9.3 Anthropic Claude 配置

#### 9.3.1 获取 API Key

1. 访问 [Anthropic 控制台](https://console.anthropic.com/)
2. 注册/登录账号
3. 获取 API Key

#### 9.3.2 配置文件

```yaml
model:
  provider: "anthropic"
  api_key: "sk-ant-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "claude-3-opus-20240229"  # 或 claude-3-sonnet
  max_tokens: 2048
```

### 9.4 Google Gemini 配置

#### 9.4.1 获取 API Key

1. 访问 [Google AI Studio](https://makersuite.google.com/app/apikey)
2. 登录 Google 账号
3. 创建 API Key

#### 9.4.2 配置文件

```yaml
model:
  provider: "google"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "gemini-pro"
```

### 9.5 阿里通义千问配置

#### 9.5.1 获取 API Key

1. 访问 [阿里云百炼](https://bailian.console.aliyun.com/)
2. 登录阿里云账号
3. 开通 DashScope 服务
4. 创建 API Key

#### 9.5.2 配置文件

```yaml
model:
  provider: "dashscope"
  api_key: "sk-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "qwen-max"  # 或 qwen-plus, qwen-turbo
```

### 9.6 百度文心一言配置

#### 9.6.1 获取 API Key

1. 访问 [百度智能云](https://cloud.baidu.com/)
2. 注册/登录账号
3. 开通文心一言服务
4. 获取 API Key 和 Secret Key

#### 9.6.2 配置文件

```yaml
model:
  provider: "wenxin"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  secret_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "ernie-bot-4"
```

### 9.7 模型选择建议

| 使用场景 | 推荐模型 | 理由 |
|---------|---------|------|
| **代码生成** | GPT-4 / Claude 3 | 代码能力强，逻辑清晰 |
| **中文内容** | 通义千问 / 文心一言 | 中文理解好，本地化佳 |
| **性价比** | GPT-3.5 / Qwen-Turbo | 价格低，速度快 |
| **复杂任务** | GPT-4 / Claude 3 Opus | 能力强，准确率高 |
| **创意写作** | Claude 3 | 文笔流畅，创意丰富 |

---

## 10. 联网搜索配置

### 10.1 支持的搜索引擎

| 搜索引擎 | 状态 | 配置难度 | 免费额度 |
|---------|------|---------|---------|
| **Google** | ✅ 已支持 | ⭐⭐⭐ | 100 次/天 |
| **Bing** | ✅ 已支持 | ⭐⭐ | 1000 次/月 |
| **百度** | ✅ 已支持 | ⭐⭐ | 有限 |
| **Tavily** | ✅ 已支持 | ⭐ | 1000 次/月 |

### 10.2 Google Custom Search 配置

#### 10.2.1 获取 API Key

1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 创建项目
3. 启用 Custom Search API
4. 创建 API Key

#### 10.2.2 创建搜索引擎

1. 访问 [Programmable Search Engine](https://programmablesearchengine.google.com/)
2. 创建新搜索引擎
3. 获取 `Search Engine ID` (cx)

#### 10.2.3 配置文件

```yaml
search:
  enabled: true
  provider: "google"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  search_engine_id: "xxxxxxxxxxxxx"
```

### 10.3 Bing Search 配置

#### 10.3.1 获取 API Key

1. 访问 [Azure Portal](https://portal.azure.com/)
2. 创建 Bing Search 资源
3. 获取 API Key

#### 10.3.2 配置文件

```yaml
search:
  enabled: true
  provider: "bing"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  endpoint: "https://api.bing.microsoft.com/v7.0/search"
```

### 10.4 Tavily Search 配置

#### 10.4.1 获取 API Key

1. 访问 [Tavily](https://tavily.com/)
2. 注册账号
3. 获取 API Key

#### 10.4.2 配置文件

```yaml
search:
  enabled: true
  provider: "tavily"
  api_key: "tvly-xxxxxxxxxxxxxxxxxxxxxxxx"
```

---

## 11. 配置文件详解

### 11.1 完整配置示例

```yaml
# OpenClaw 完整配置文件

# 应用配置
app:
  name: "OpenClaw"
  version: "1.0.0"
  debug: false
  log_level: "INFO"
  log_file: "logs/openclaw.log"

# 模型配置
model:
  provider: "openai"
  api_key: "sk-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "gpt-4"
  base_url: "https://api.openai.com/v1"
  temperature: 0.7
  max_tokens: 2048
  timeout: 30

# 渠道配置
channel:
  # 飞书
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    verification_token: "xxxxxxxxxxxxxxxxxxxxxxxx"
  
  # 钉钉
  dingtalk:
    enabled: false
    app_key: "xxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    webhook: "https://oapi.dingtalk.com/robot/send?access_token=xxx"
  
  # 企业微信
  wecom:
    enabled: false
    corp_id: "wwxxxxxxxxxxxx"
    agent_id: 1000001
    secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
  
  # Telegram
  telegram:
    enabled: false
    bot_token: "xxxxxxxxx:xxxxxxxxxxxxxxxxxxxxxxxxxxx"

# 搜索配置
search:
  enabled: true
  provider: "google"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  search_engine_id: "xxxxxxxxxxxxx"

# 数据库配置
database:
  type: "sqlite"
  path: "data/openclaw.db"
  # 或使用 MySQL
  # type: "mysql"
  # host: "localhost"
  # port: 3306
  # user: "openclaw"
  # password: "your-password"
  # database: "openclaw"

# 定时任务配置
scheduler:
  enabled: true
  timezone: "Asia/Shanghai"
  tasks:
    - name: "daily_report"
      cron: "0 8 * * *"
      handler: "report.daily"
    - name: "weekly_summary"
      cron: "0 9 * * 1"
      handler: "report.weekly"

# Skills 配置
skills:
  enabled: true
  paths:
    - "skills/builtin"
    - "skills/custom"
  
  # 自定义技能配置
  custom_skill_name:
    enabled: true
    config_key: "config_value"

# 安全配置
security:
  api_tokens:
    - "your-api-token-1"
    - "your-api-token-2"
  
  ip_whitelist:
    - "127.0.0.1"
    - "192.168.1.0/24"

# 性能配置
performance:
  max_concurrent_tasks: 10
  task_timeout: 300
  cache_enabled: true
  cache_ttl: 3600
```

### 11.2 环境变量配置

也可以使用环境变量覆盖配置文件：

```bash
# .env 文件
OPENCLAW_MODEL_PROVIDER=openai
OPENCLAW_MODEL_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx
OPENCLAW_MODEL_MODEL_NAME=gpt-4
OPENCLAW_CHANNEL_FEISHU_APP_ID=cli_xxxxxxxxxxxxx
OPENCLAW_CHANNEL_FEISHU_APP_SECRET=xxxxxxxxxxxxxxxxxxxxxxxx
```

### 11.3 配置优先级

**优先级从高到低**:
1. 命令行参数
2. 环境变量
3. config.yaml 配置文件
4. 默认值

---

## 12. 常见问题

### 12.1 安装问题

#### Q1: pip install 报错

**问题**: `ERROR: Could not install packages due to an EnvironmentError`

**解决**:
```bash
# 使用国内镜像
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

# 或使用 --user 参数
pip install --user -r requirements.txt
```

#### Q2: Python 版本不兼容

**问题**: `SyntaxError: invalid syntax`

**解决**:
```bash
# 检查 Python 版本
python3 --version

# OpenClaw 需要 Python 3.8+
# 如果版本过低，请升级 Python
```

### 12.2 配置问题

#### Q3: 配置文件找不到

**问题**: `FileNotFoundError: config.yaml not found`

**解决**:
```bash
# 复制示例配置
cp config.example.yaml config.yaml

# 或指定配置文件路径
python3 -m openclaw --config /path/to/config.yaml
```

#### Q4: API Key 无效

**问题**: `Invalid API Key` 或 `401 Unauthorized`

**解决**:
1. 检查 API Key 是否正确复制（无多余空格）
2. 确认 API Key 未过期
3. 确认账号有足够的额度
4. 检查网络是否需要代理

### 12.3 渠道问题

#### Q5: 飞书机器人收不到消息

**问题**: 消息发送到飞书群，机器人无响应

**解决**:
1. 检查机器人是否已添加到群聊
2. 检查事件订阅配置是否正确
3. 检查 Verification Token 是否匹配
4. 查看日志确认是否收到回调

#### Q6: 钉钉机器人推送失败

**问题**: `400 invalid signature`

**解决**:
```yaml
# 检查加签密钥是否正确
channel:
  dingtalk:
    secret: "SECxxxxxxxxxxxxxxxxxxxxxxxx"  # 包含 SEC 前缀
```

### 12.4 模型问题

#### Q7: GPT-4 调用失败

**问题**: `Rate limit exceeded` 或 `Quota exceeded`

**解决**:
1. 检查 API Key 是否有 GPT-4 权限
2. 检查是否超过速率限制
3. 检查账户余额是否充足
4. 考虑降级使用 GPT-3.5

#### Q8: 响应速度太慢

**问题**: 模型响应时间超过 30 秒

**解决**:
```yaml
# 降低 max_tokens
model:
  max_tokens: 1024  # 从 2048 降低

# 或使用更快的模型
model:
  model_name: "gpt-3.5-turbo"  # 从 gpt-4 降级
```

### 12.5 性能问题

#### Q9: 内存占用过高

**问题**: 服务运行一段时间后内存超过 2GB

**解决**:
```yaml
# 限制并发任务数
performance:
  max_concurrent_tasks: 5

# 启用缓存
performance:
  cache_enabled: true
  cache_ttl: 1800  # 30 分钟
```

---

## 附录 A: 37 个章节完整目录

### Day1-龙虾机器人
- 链接：#HXyqdSbZOoHvq8xh7CzclHTmnoR

### 第 1 章 AI 基础知识普及
- 链接：#DcAtd1EUgoRsvfxOadKceOo2nRf
  - 1.AI 编程产品分类 #LfLLdWN2BoAPk3xDuJScHSJQnQ2
  - 2.AI 编程主流模型 #VWVsd7Z5ooDr7nxPWKtcHFrpnfe
    - 2.1 国际 AI 编程工具最新模型 #UTYwdZp8yofddBxpEeNcknCvnqh
    - 2.2 国内 AI 编程工具最新模型 #Jos5dCoZpo8VzYxrlhNcM90vnyf
  - 3.AI 编程必知术语 #XOYNd88gyoZeWhxxE6HcyKrhnDh
    - 3.1 AI 大模型 #QfbIdkAgmo2iQLxfDXzcuUvQnpf
    - 3.2 Token #YNjNdm1Doo2ZRixgLGZcWcBSnrc
    - 3.3 提示词 #PteAd2BlToec3IxiWkVcXDs5nhh
    - 3.4 上下文长度 #HC2KdQwPAoPAhXx1wWvceWUCnSc
    - 3.5 Skills（技能）#XTiedNb70oKo0xxTX37cf3iinid
    - 3.6 MCP（模型上下文协议）#BrBZdVldlo8gGqx6bmBcZWpBnlf

### 第 2 章 龙虾机器人介绍
- 链接：#DewFdIcaiop5ayx5J8ocVfPMnYb
  - 1.龙虾的由来 #KToWdFeZToFUF0xJnrqcfbTTnFg
  - 2.龙虾为什么这么火 #GjlYdsPoIoVSoSxO1GPcP3A7ns2
  - 3.龙虾可以完成哪些工作 #OYM0dx53FocF66xJpYicnAOCnOc
    - 3.1 普通人：零门槛私人数字管家 #QvVTd6GEuo8lJkxiFklc1HcKn5b
    - 3.2 IT 从业者：技术流程效率工具 #TUp5ddkaRoZH0tx0L6Wc7lg3nmh
    - 3.3 企业：轻量化办公自动化助手 #OtkDdnst1oLrroxvlI0cmShInlf
    - 3.4 自媒体：内容运营提速工具 #ISVsdzisUoMBapx0oqCcNx4dnbh
  - 4.龙虾收费吗 #EdZxdUpUnoUyAnx7qqLc99upnPg

### 第 3 章 龙虾机器人架构
- 链接：#HzwcdvOkkoKCvlxno1vcxE8unOc
  - 1.OpenClaw 官方网址 #WF8cdJxwaoaHpKxL58xcfgJGn7g
  - 2.OpenClaw 架构组成 #QH2bdQTb0oRDPnxnAjYcsLTWnKb

### 第 4 章 龙虾机器人安装
- 链接：#CCjXdTA3wopHswx4lRZcYVCTnSe
  - 1.龙虾机器人部署方式 #R3vtd8Ew5oky93x0jJpcakXmnth
  - 2.本地部署 #IshFdK2M7ordD9xbUllcVuDxnuf
  - 3.云端部署 #FMMRdupS8oVwYPxTNBecs0cunaf

### 第 5 章 龙虾机器人配置聊天渠道
- 链接：#VgrndQpPao06ZPxNzGnc1YYbnzd
  - 1.飞书渠道 #G7rldXapBoMO4FxBN9UcB1n2nXo
  - 2.钉钉渠道 #XicgdrHLzoRuHyx7I3rc4oIknVf
  - 3.电报渠道 #AhMfdARE6oWDjuxB5GLcMKq8nnd
  - 4.QQ 机器人渠道 #Yrfdd2U9aoGypxxfnQtcqyQJnib
  - 5.企业微信渠道 #PEHfd6elUookFSxVGqQc2SXcnDh

### 第 6 章 龙虾机器人模型配置
- 链接：#OK0fd2vAHoHBEkxP6wAcfKZpnbc
  - 1.对接国内模型 #WHIcdM6lHoibJAx9s6RcOG8hnEf

---

## 附录 B: 核心概念详解

### 提示词编写技巧

**公式**: 具体任务 + 约束条件 + 输出要求

**示例**:
```
❌ 笼统：帮我写个 Python 脚本
✅ 具体：帮我写个 Python 脚本，功能是批量重命名文件夹里的 JPG 图片，
        按日期排序，保留原文件名作为前缀，添加中文注释说明每行代码的作用
```

### 上下文长度理解

**类比**: 短期记忆力上限

**影响因素**:
- Token 数量限制
- 模型架构设计

**优化建议**:
- 分段提交长代码
- 关键信息前置
- 重要逻辑重复强调

---

## 附录 C: Skills vs MCP 关系图

```
┌─────────────────────────────────────────────┐
│           AI 大模型                          │
│  ┌─────────────────────────────────────┐    │
│  │  Skills（专项能力插件包）             │    │
│  │  • 代码生成 Skill                    │    │
│  │  • Bug 排查 Skill                    │    │
│  │  • SQL 编写 Skill                    │    │
│  │  • 接口调试 Skill                    │    │
│  │  • 注释生成 Skill                    │    │
│  └─────────────────────────────────────┘    │
│                    ↕                        │
│  ┌─────────────────────────────────────┐    │
│  │  MCP（模型上下文协议）                │    │
│  │  = AI 世界的"USB-C 统一接口"          │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
                    ↕
    ┌───────────────┼───────────────┐
    ↓               ↓               ↓
┌───────┐    ┌──────────┐    ┌──────────┐
│数据库  │    │代码仓库   │    │本地文件   │
└───────┘    └──────────┘    └──────────┘
```

**配合效果**:
1. MCP 打通连接通道（USB-C 接口）
2. Skills 执行具体任务（插在 USB-C 上的设备）
3. AI 突破自身局限，调用外部资源
4. 完成更复杂的编程任务

---

**文档版本**: v3.0（完整合并版）  
**创建时间**: 2026-03-22  
**最后更新**: 2026-03-22  
**总章节**: 12 章 + 3 个附录  
**总字数**: 约 15,000 字
