# 🦞 OpenClaw 龙虾机器人 - 飞书文档完整内容

> **来源**: 老男孩 AI 编程实战第一期  
> **最新修改**: 2026-03-22  
> **飞书文档**: https://my.feishu.cn/wiki/AlBuwnaeTidXVOkT96gcuavrn8b

---

## 📑 完整目录

### Day1-龙虾机器人
- [Day1-龙虾机器人](#day1-龙虾机器人)

### 第 1 章 AI 基础知识普及
- [1. AI 编程产品分类](#1-ai-编程产品分类)
- [2. AI 编程主流模型](#2-ai-编程主流模型)
  - [2.1 国际 AI 编程工具最新模型](#21-国际 AI 编程工具最新模型)
  - [2.2 国内 AI 编程工具最新模型](#22-国内 AI 编程工具最新模型)
- [3. AI 编程必知术语](#3-ai-编程必知术语)
  - [3.1 AI 大模型](#31-ai-大模型)
  - [3.2 Token](#32-token)
  - [3.3 提示词](#33-提示词)
  - [3.4 上下文长度](#34-上下文长度)
  - [3.5 Skills（技能）](#35-skills 技能)
  - [3.6 MCP（模型上下文协议）](#36-mcp 模型上下文协议)

### 第 2 章 龙虾机器人介绍
- [1. 龙虾的由来](#1-龙虾的由来)
- [2. 龙虾为什么这么火](#2-龙虾为什么这么火)
- [3. 龙虾可以完成哪些工作](#3-龙虾可以完成哪些工作)
  - [3.1 普通人：零门槛私人数字管家](#31-普通人零门槛私人数字管家)
  - [3.2 IT 从业者：技术流程效率工具](#32-it-从业者技术流程效率工具)
  - [3.3 企业：轻量化办公自动化助手](#33-企业轻量化办公自动化助手)
  - [3.4 自媒体：内容运营提速工具](#34-自媒体内容运营提速工具)
- [4. 龙虾收费吗](#4-龙虾收费吗)

### 第 3 章 龙虾机器人架构
- [1. OpenClaw 官方网址](#1-openclaw-官方网址)
- [2. OpenClaw 架构组成](#2-openclaw-架构组成)

### 第 4 章 龙虾机器人安装
- [1. 龙虾机器人部署方式](#1-龙虾机器人部署方式)
- [2. 本地部署](#2-本地部署)
- [3. 云端部署](#3-云端部署)

### 第 5 章 龙虾机器人配置聊天渠道
- [1. 飞书渠道](#1-飞书渠道)
- [2. 钉钉渠道](#2-钉钉渠道)
- [3. 电报渠道](#3-电报渠道)
- [4. QQ 机器人渠道](#4-qq-机器人渠道)
- [5. 企业微信渠道](#5-企业微信渠道)

### 第 6 章 龙虾机器人模型配置
- [1. 对接国内模型](#1-对接国内模型)

---

## Day1-龙虾机器人

**最新修改时间**: 2026-03-22

---

## 第 1 章 AI 基础知识普及

### 1. AI 编程产品分类

| 大类分类 | 核心工具 | 核心特点 | 适用场景 |
|---------|---------|---------|---------|
| **Chat 聊天型** | OpenAI: ChatGPT<br>Anthropic: Claude<br>Google: Gemini | 自然语言对话，无专属编程环境，轻量化问答，零门槛 | 代码咨询、片段生成、Bug 排查、思路梳理 |
| **IDE 集成型** | Kiro<br>Cursor<br>Antigravity | 原生 AI IDE，沉浸式编码，实时补全、调试、项目级辅助 | 专业项目开发、日常编码、全栈工程编写 |
| **CLI 命令行型** | OpenAI: Codex<br>Anthropic: Claude Code | 纯终端交互，无图形界面，高效批量处理、自动化运维 | 服务器开发、命令行批量操作、自动化部署 |

### 2. AI 编程主流模型

#### 2.1 国际 AI 编程工具最新模型

| 厂商 | 系列 | 模型 |
|------|------|------|
| **OpenAI** | ChatGPT、Codex | GPT-5.4<br>GPT-5.3-Codex |
| **Anthropic** | ClaudeCode | Claude Opus 4.6<br>Claude Sonnet 4.6 |
| **Google** | Gemini | Gemini 3.1 Pro<br>大香蕉 |

#### 2.2 国内 AI 编程工具最新模型

| 厂商 | 系列 | 模型 |
|------|------|------|
| **阿里** | 通义千问 Qwen | Qwen 2.5 Code |
| **DeepSeek** | DeepSeek-Coder | DeepSeek-Coder V3 |

### 3. AI 编程必知术语

#### 3.1 AI 大模型

**定义**: 基于深度学习技术的大规模语言模型，能够理解和生成自然语言

**特点**:
- 参数量巨大（数十亿到数千亿）
- 训练数据海量
- 具备强大的语言理解和生成能力
- 支持多种任务（问答、写作、编程等）

#### 3.2 Token

**定义**: AI 大模型处理文本的基本单位

**说明**:
- 英文：1 个单词≈1-3 个 Token
- 中文：1 个汉字≈1-2 个 Token
- 计费单位：按 Token 数量计费
- 上下文长度：模型一次能处理的最大 Token 数

#### 3.3 提示词

**定义**: 发送给 AI 大模型的指令或问题

**编写原则**:
- 不能太笼统，越具体越好用
- 明确任务目标
- 提供必要的上下文信息
- 指定输出格式

**优秀示例**:
```
帮我排查这段 Java 代码的空指针异常，保留原有业务逻辑，逐行添加易懂的中文注释
```

#### 3.4 上下文长度

**定义**: AI 大模型的短期记忆力上限，计量单位 Token

**问题**:
- 上下文太短 → AI 会"断片儿"
- 忘记之前的对话内容
- 无法处理超长代码或文档

**优化建议**:
- 分段提交长代码
- 关键信息前置
- 定期总结对话要点

#### 3.5 Skills（技能）

**定义**: 给 AI 大模型定制的专项能力插件包

**类型**:
- 代码生成 Skill
- Bug 排查 Skill
- SQL 编写 Skill
- 接口调试 Skill
- 注释生成 Skill

**优势**:
- 提升结果专业性
- 避免输出偏离需求
- 可复用最佳实践

#### 3.6 MCP（模型上下文协议）

**全称**: Model Context Protocol

**定义**: AI 世界的"USB-C 统一接口"

**解决的问题**:
- 无需重复开发适配逻辑
- 统一连接外部工具
- 标准化数据交换格式

**应用场景**:
- 连接数据库
- 访问代码仓库
- 读取本地文件
- 调用外部 API

---

## 第 2 章 龙虾机器人介绍

### 1. 龙虾的由来

**品牌演变历史**:

| 阶段 | 名称 | 原因 |
|------|------|------|
| 最初 | Clawdbot | 原始名称 |
| 第一次改名 | Moltbot | 避免与 Claude 发音相似，版权纠纷 |
| 最终名称 | OpenClaw | 仅过了三天又改名 |

**品牌寓意**:
- Claw = 爪子或者龙虾的鳌 🦞
- 选择龙虾的原因：作者家乡盛产龙虾，给家乡代言

### 2. 龙虾为什么这么火

**市场痛点分析**:

| AI 产品类型 | 优势 | 劣势 |
|------------|------|------|
| **网页聊天 AI**<br>(DeepSeek、豆包、千问) | 随时随地访问 | ❌ 无法访问本地文件<br>❌ 无法安装软件<br>❌ 与电脑环境隔离 |
| **编程 AI 助手**<br>(ClaudeCode、Codex) | 可以接管电脑环境<br>可以安装软件 | ❌ 必须在电脑面前<br>❌ 离开电脑就指挥不了 |

**核心痛点**: 鱼和熊掌不可兼得

**龙虾解决方案**: 解决了无法随时随地在任意地方指挥家里的 AI 干活的痛点

### 3. 龙虾可以完成哪些工作

#### 3.1 普通人：零门槛私人数字管家

**核心价值**: 零门槛使用 AI 能力

**典型场景**:
- 日常任务管理
- 信息查询
- 日程安排
- 生活助手

#### 3.2 IT 从业者：技术流程效率工具

**核心价值**: 提升技术工作效率

**典型场景**:
- 代码生成
- 自动化脚本
- 技术文档编写
- Bug 排查
- 代码审查

#### 3.3 企业：轻量化办公自动化助手

**核心价值**: 降低办公自动化门槛

**典型场景**:
- 工作流程自动化
- 数据报表生成
- 客服响应
- 内部培训
- 知识管理

#### 3.4 自媒体：内容运营提速工具

**核心价值**: 提升内容创作效率

**典型场景**:
- 选题素材收集
- 内容排版
- 运营分发
- 数据复盘
- 热点追踪

### 4. 龙虾收费吗

**开源协议**: MIT License（免费开源）

**费用说明**:
- OpenClaw 软件本身：免费
- 使用大模型服务：需要付费（按 Token 计费）
- 本地部署：免费（使用自己的 API Key）
- 云端部署：可能需要服务器费用

---

## 第 3 章 龙虾机器人架构

### 1. OpenClaw 官方网址

- **官方网站**: https://docs.openclaw.ai/
- **GitHub**: https://github.com/openclaw/openclaw
- **Discord**: https://discord.com/invite/clawd
- **文档**: https://docs.openclaw.ai/zh-CN

### 2. OpenClaw 架构组成

**整体架构**:

```
┌─────────────────────────────────────────────┐
│           用户界面层                          │
│  ┌─────────┬─────────┬─────────┬─────────┐  │
│  │  飞书   │  钉钉   │ Telegram│  微信   │  │
│  └─────────┴─────────┴─────────┴─────────┘  │
└─────────────────────────────────────────────┘
                    ↕
┌─────────────────────────────────────────────┐
│           OpenClaw 核心层                     │
│  ┌─────────────────────────────────────┐    │
│  │  Skills 系统（技能插件）               │    │
│  │  • 代码生成 • Bug 排查 • SQL 编写     │    │
│  │  • 接口调试 • 注释生成 • 文档生成     │    │
│  └─────────────────────────────────────┘    │
│                    ↕                        │
│  ┌─────────────────────────────────────┐    │
│  │  MCP（模型上下文协议）                 │    │
│  │  = AI 世界的"USB-C 统一接口"          │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
                    ↕
┌─────────────────────────────────────────────┐
│           大模型层                            │
│  ┌─────────┬─────────┬─────────┬─────────┐  │
│  │ GPT-4   │ Claude  │ Gemini  │ 通义千问 │  │
│  └─────────┴─────────┴─────────┴─────────┘  │
└─────────────────────────────────────────────┘
                    ↕
    ┌───────────────┼───────────────┐
    ↓               ↓               ↓
┌───────┐    ┌──────────┐    ┌──────────┐
│数据库  │    │代码仓库   │    │本地文件   │
└───────┘    └──────────┘    └──────────┘
```

**核心组件**:
1. **渠道适配器**: 支持多种聊天平台
2. **Skills 系统**: 可扩展的技能插件
3. **MCP 协议**: 连接外部工具
4. **模型适配器**: 支持多种大模型
5. **任务调度器**: 定时任务管理

---

## 第 4 章 龙虾机器人安装

### 1. 龙虾机器人部署方式

| 部署方式 | 优点 | 缺点 | 适用场景 |
|---------|------|------|---------|
| **本地部署** | 数据私密、完全控制、免费 | 需要服务器资源、自行维护 | 个人使用、小企业 |
| **云端部署** | 免维护、高可用、弹性扩展 | 需要付费、数据在云端 | 企业用户、大规模使用 |
| **Docker 部署** | 环境隔离、一键部署、易迁移 | 需要 Docker 基础 | 推荐方案 |

### 2. Windows 本地部署（重点）⭐

#### 2.1 环境准备

**系统要求**:
- 操作系统：Windows 10/11（64 位）
- 内存：4GB+（推荐 8GB+）
- 磁盘：20GB+ 可用空间
- Python: 3.8 或更高版本
- Git: 最新版本

**步骤 1: 安装 Python**

1. 访问 Python 官网：https://www.python.org/downloads/
2. 下载 Python 3.8+ 安装包（选择 Windows x86-64 executable installer）
3. **重要**: 安装时勾选 "Add Python to PATH"
4. 点击 "Install Now" 完成安装

**验证 Python 安装**:
```cmd
# 打开命令提示符（CMD）或 PowerShell
python --version
# 应显示：Python 3.x.x

pip --version
# 应显示：pip x.x.x
```

**步骤 2: 安装 Git**

1. 访问 Git 官网：https://git-scm.com/download/win
2. 下载 Windows 版 Git 安装包
3. 双击运行安装程序
4. 一路点击 "Next" 使用默认设置即可

**验证 Git 安装**:
```cmd
git --version
# 应显示：git version 2.x.x
```

#### 2.2 克隆 OpenClaw 仓库

**方式一：使用 Git 克隆**
```cmd
# 创建项目目录
cd C:\Users\你的用户名\Documents

# 克隆仓库
git clone https://github.com/cmdop/openclaw.git

# 进入项目目录
cd openclaw
```

**方式二：手动下载 ZIP**
1. 访问 https://github.com/cmdop/openclaw
2. 点击 "Code" → "Download ZIP"
3. 下载到本地并解压
4. 在解压目录打开命令提示符

#### 2.3 创建 Python 虚拟环境

```cmd
# 在项目目录下执行
# 创建虚拟环境
python -m venv venv

# 激活虚拟环境
venv\Scripts\activate

# 激活成功后，命令行前面会显示 (venv)
```

**常见激活问题**:
- 如果提示"无法加载脚本"，需要修改 PowerShell 执行策略：
  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```
- 然后重新激活：`venv\Scripts\activate`

#### 2.4 安装依赖

```cmd
# 确保已激活虚拟环境（命令行前有 (venv)）
# 升级 pip
python -m pip install --upgrade pip

# 安装依赖
pip install -r requirements.txt

# 安装可能需要几分钟，等待完成
```

**常见问题**:
- 如果安装失败，可能是网络问题，可以使用国内镜像：
  ```cmd
  pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
  ```

#### 2.5 配置 OpenClaw

```cmd
# 复制配置文件
copy config.example.yaml config.yaml

# 编辑配置文件（使用记事本或 VS Code）
notepad config.yaml
```

**配置文件示例** (config.yaml):
```yaml
# 应用配置
app:
  name: "OpenClaw"
  version: "1.0.0"
  debug: false

# 模型配置（以 OpenAI 为例）
model:
  provider: "openai"
  api_key: "sk-你的 API Key"
  model_name: "gpt-4"
  base_url: "https://api.openai.com/v1"

# 渠道配置（以飞书为例）
channel:
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    verification_token: "xxxxxxxxxxxxxxxxxxxxxxxx"
```

**获取 API Key**:
- OpenAI: https://platform.openai.com/api-keys
- 通义千问：https://dashscope.console.aliyun.com/
- DeepSeek: https://platform.deepseek.com/

#### 2.6 启动 OpenClaw

```cmd
# 确保已激活虚拟环境
# 启动 OpenClaw
python -m openclaw

# 或使用 python 直接运行
python openclaw/main.py
```

**启动成功标志**:
```
[INFO] OpenClaw is starting...
[INFO] Loading configuration...
[INFO] Connecting to Feishu...
[INFO] Server started on http://localhost:8080
[INFO] OpenClaw is ready!
```

#### 2.7 后台运行（可选）

**方式一：使用 start 命令**
```cmd
start python -m openclaw
# 会打开新窗口运行
```

**方式二：使用 VBScript 后台运行**
1. 创建 `run_openclaw.vbs` 文件：
   ```vbs
   Set objShell = CreateObject("WScript.Shell")
   objShell.Run "python -m openclaw", 0, False
   ```
2. 双击运行 `run_openclaw.vbs`

**方式三：使用 NSSM 注册为 Windows 服务**
1. 下载 NSSM: https://nssm.cc/download
2. 解压后打开命令提示符（管理员）
3. 运行：`nssm install OpenClaw`
4. 配置:
   - Path: `C:\Python39\python.exe`
   - Startup directory: `C:\Users\你的用户名\Documents\openclaw`
   - Arguments: `-m openclaw`
5. 点击 "Install service"
6. 启动服务：`nssm start OpenClaw`

#### 2.8 停止 OpenClaw

```cmd
# 在运行窗口按 Ctrl+C 停止
# 或强制结束进程
taskkill /F /IM python.exe

# 如果使用 NSSM 服务
nssm stop OpenClaw
```

### 3. Linux/Mac 本地部署

**环境要求**:
- Python 3.8+
- Git
- 4GB+ 内存
- 20GB+ 磁盘空间

**安装步骤**:
```bash
# 1. 克隆仓库
git clone https://github.com/cmdop/openclaw.git
cd openclaw

# 2. 创建虚拟环境
python3 -m venv venv
source venv/bin/activate  # Linux/Mac

# 3. 安装依赖
pip install -r requirements.txt

# 4. 配置
cp config.example.yaml config.yaml
vim config.yaml

# 5. 启动
python3 -m openclaw
```

### 4. 云端部署

**部署平台**:
- 阿里云
- 腾讯云
- 华为云
- AWS
- Azure

**部署步骤**:
1. 购买云服务器（2 核 4G 起步）
2. 安装 Docker
3. 拉取 OpenClaw 镜像
4. 配置环境变量
5. 启动容器
6. 配置域名和 HTTPS

---

## 第 5 章 龙虾机器人配置聊天渠道

### 1. 飞书渠道

**配置步骤**:
1. 登录飞书开发者后台
2. 创建企业自建应用
3. 获取 App ID 和 App Secret
4. 配置事件订阅
5. 配置机器人权限
6. 发布应用

**配置文件**:
```yaml
channel:
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    verification_token: "xxxxxxxxxxxxxxxxxxxxxxxx"
```

### 2. 钉钉渠道

**配置步骤**:
1. 登录钉钉开发者后台
2. 创建企业内部应用
3. 获取 AppKey 和 AppSecret
4. 配置事件订阅
5. 配置机器人权限

**配置文件**:
```yaml
channel:
  dingtalk:
    enabled: true
    app_key: "xxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
```

### 3. 电报渠道

**配置步骤**:
1. 联系 @BotFather 创建机器人
2. 获取 Bot Token
3. 配置 Webhook

**配置文件**:
```yaml
channel:
  telegram:
    enabled: true
    bot_token: "xxxxxxxxx:xxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### 4. QQ 机器人渠道

**配置步骤**:
1. 使用 OneBot 协议
2. 配置反向 WebSocket
3. 获取访问 Token

**配置文件**:
```yaml
channel:
  qq:
    enabled: true
    ws_reverse_url: "ws://127.0.0.1:8080"
    access_token: "xxxxxxxxxxxxxxxx"
```

### 5. 企业微信渠道

**配置步骤**:
1. 登录企业微信管理后台
2. 创建自建应用
3. 获取 CorpID 和 Secret
4. 配置接收消息

**配置文件**:
```yaml
channel:
  wecom:
    enabled: true
    corp_id: "wwxxxxxxxxxxxx"
    agent_id: "1000001"
    secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
    token: "xxxxxxxxxxxxxxxx"
```

---

## 第 6 章 龙虾机器人模型配置

### 1. 对接国内模型

#### 1.1 通义千问（阿里）

**配置文件**:
```yaml
model:
  provider: "qwen"
  api_key: "sk-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "qwen-max"
  base_url: "https://dashscope.aliyuncs.com/api/v1"
```

#### 1.2 DeepSeek

**配置文件**:
```yaml
model:
  provider: "deepseek"
  api_key: "sk-xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "deepseek-coder"
  base_url: "https://api.deepseek.com/v1"
```

#### 1.3 文心一言（百度）

**配置文件**:
```yaml
model:
  provider: "ernie"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  secret_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  model_name: "ernie-bot-4"
```

#### 1.4 讯飞星火

**配置文件**:
```yaml
model:
  provider: "spark"
  app_id: "xxxxxxxx"
  api_key: "xxxxxxxxxxxxxxxxxxxxxxxx"
  api_secret: "xxxxxxxxxxxxxxxxxxxxxxxx"
```

---

## 附录：37 个章节完整目录

### Day1-龙虾机器人
- Day1-龙虾机器人

### 第 1 章 AI 基础知识普及
1. AI 编程产品分类
2. AI 编程主流模型
   - 2.1 国际 AI 编程工具最新模型
   - 2.2 国内 AI 编程工具最新模型
3. AI 编程必知术语
   - 3.1 AI 大模型
   - 3.2 Token
   - 3.3 提示词
   - 3.4 上下文长度
   - 3.5 Skills（技能）
   - 3.6 MCP（模型上下文协议）

### 第 2 章 龙虾机器人介绍
1. 龙虾的由来
2. 龙虾为什么这么火
3. 龙虾可以完成哪些工作
   - 3.1 普通人：零门槛私人数字管家
   - 3.2 IT 从业者：技术流程效率工具
   - 3.3 企业：轻量化办公自动化助手
   - 3.4 自媒体：内容运营提速工具
4. 龙虾收费吗

### 第 3 章 龙虾机器人架构
1. OpenClaw 官方网址
2. OpenClaw 架构组成

### 第 4 章 龙虾机器人安装
1. 龙虾机器人部署方式
2. 本地部署
3. 云端部署

### 第 5 章 龙虾机器人配置聊天渠道
1. 飞书渠道
2. 钉钉渠道
3. 电报渠道
4. QQ 机器人渠道
5. 企业微信渠道

### 第 6 章 龙虾机器人模型配置
1. 对接国内模型

---

**文档版本**: v1.0  
**创建时间**: 2026-03-22  
**总章节数**: 37 个  
**文档来源**: 飞书云文档 - 老男孩 AI 编程实战第一期
