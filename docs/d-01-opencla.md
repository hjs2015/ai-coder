# d-01-opencla - 龙虾机器人 (OpenClaw) 详解

**文档版本**: v1.0  
**创建时间**: 2026-03-22  
**来源**: 老男孩 AI 编程实战第一期 - 飞书云文档  
**文档 URL**: https://my.feishu.cn/wiki/AlBuwnaeTidXVOkT96gcuavrn8b

---

## 📖 目录

- [1. 龙虾的由来](#1-龙虾的由来)
- [2. 龙虾为什么这么火](#2-龙虾为什么这么火)
- [3. 龙虾可以完成哪些工作](#3-龙虾可以完成哪些工作)
- [4. 龙虾收费吗](#4-龙虾收费吗)
- [5. OpenClaw 架构组成](#5-openclaw-架构组成)
- [6. 部署方式](#6-部署方式)
- [7. 聊天渠道配置](#7-聊天渠道配置)
- [8. 模型配置](#8-模型配置)

---

## 1. 龙虾的由来

### 1.1 名称来源

**OpenClaw** 中文名"**龙虾机器人**"，取名自：
- **Open** - 开源开放
- **Claw** - 爪子（龙虾的钳子）

寓意：像龙虾一样灵活抓取各种 AI 能力，为用户提供服务。

### 1.2 项目背景

随着 AI 大模型的快速发展，普通人使用 AI 的门槛依然存在：
- ❌ 需要学习复杂的提示词工程
- ❌ 需要在多个 AI 工具之间切换
- ❌ 无法将 AI 能力集成到日常工作流程
- ❌ 缺乏个性化的 AI 助手

**OpenClaw 应运而生**：
- ✅ 零门槛使用 AI
- ✅ 统一接口对接多个 AI 模型
- ✅ 通过聊天工具（飞书/钉钉/微信）直接交互
- ✅ 支持自定义技能扩展

---

## 2. 龙虾为什么这么火

### 2.1 核心优势

| 优势 | 说明 | 传统方案对比 |
|------|------|-------------|
| **零门槛** | 无需编程基础，聊天即可使用 | 需要学习 Python/API 调用 |
| **多渠道** | 支持飞书/钉钉/微信/QQ/电报 | 单一平台限制 |
| **多模型** | 同时对接 GPT/Claude/通义千问等 | 绑定单一 AI 厂商 |
| **可扩展** | Skills 技能系统，自由扩展功能 | 功能固定，无法定制 |
| **私有化** | 支持本地部署，数据自主可控 | 云端 SaaS，数据不可控 |

### 2.2 火爆原因分析

1. **AI 普及需求爆发**
   - 2026 年 AI 大模型成熟，普通人急需使用工具
   - 传统 AI 工具学习成本高，龙虾降低门槛

2. **企业数字化转型**
   - 企业需要轻量化 AI 助手
   - 龙虾可快速部署到企业微信/钉钉

3. **开源生态优势**
   - 社区贡献 Skills 技能
   - 持续迭代更新

4. **CoPaw 技能生态**
   - 107+ 现成技能可直接使用
   - 涵盖 Web/DevOps/安全/数据分析等领域

---

## 3. 龙虾可以完成哪些工作

### 3.1 普通人：零门槛私人数字管家

**典型场景**:

| 场景 | 使用方式 | 效果 |
|------|---------|------|
| **日程管理** | "@龙虾 明天上午 10 点提醒我开会" | 自动创建提醒 |
| **天气查询** | "北京今天天气怎么样" | 返回天气信息 + 穿衣建议 |
| **新闻推送** | "每天早上 8 点推送新闻联播" | 定时推送 CCTV 新闻 |
| **股票监控** | "宁德时代股价超过 200 元提醒我" | 股价预警通知 |
| **文档总结** | 上传 PDF 文件 "帮我总结这个文档" | 返回核心内容摘要 |
| **翻译助手** | "把这段话翻译成英文" | 高质量翻译 |

**价值**:
- ⏰ 每天节省 1-2 小时信息处理时间
- 📱 一个聊天窗口搞定所有需求
- 🤖 7x24 小时在线私人助理

### 3.2 IT 从业者：技术流程效率工具

**典型场景**:

| 场景 | 使用方式 | 效果 |
|------|---------|------|
| **代码生成** | "用 Python 写一个文件批量重命名脚本" | 返回完整代码 + 使用说明 |
| **Bug 排查** | 粘贴错误日志 "这个错误怎么解决" | 定位问题 + 解决方案 |
| **Git 操作** | "帮我创建一个 Git 标签并推送" | 自动执行 Git 命令 |
| **服务器监控** | "检查 10.21.0.2 的磁盘使用率" | 返回服务器状态报告 |
| **日志分析** | 上传日志文件 "分析异常错误" | 提取关键错误信息 |
| **自动化部署** | "部署这个应用到测试环境" | 执行 CI/CD 流水线 |

**价值**:
- 💻 减少重复性编码工作 50%+
- 🐛 Bug 排查时间从小时级降至分钟级
- 🚀 自动化运维流程，降低人为错误

### 3.3 企业：轻量化办公自动化助手

**典型场景**:

| 场景 | 使用方式 | 效果 |
|------|---------|------|
| **工单处理** | "导出本周所有功能需求工单" | 生成 Excel 报表 |
| **数据报表** | "统计各部门本月考勤数据" | 自动汇总 + 可视化图表 |
| **客户跟进** | "提醒我下午 3 点回访 A 客户" | CRM 系统集成提醒 |
| **合同审核** | 上传合同 "检查风险条款" | 标记潜在法律风险 |
| **会议纪要** | 上传录音 "整理会议纪要" | 自动生成会议记录 + 待办事项 |
| **培训助手** | "新员工入职培训资料在哪里" | 快速检索企业知识库 |

**价值**:
- 📊 办公效率提升 30%+
- 💰 降低人力成本（1 个 AI 助手 = 3 个初级员工工作量）
- 📈 数据驱动决策，提升管理质量

### 3.4 自媒体：内容运营提速工具

**典型场景**:

| 场景 | 使用方式 | 效果 |
|------|---------|------|
| **选题策划** | "帮我生成 10 个 AI 相关的短视频选题" | 返回热门话题列表 |
| **文案写作** | "写一篇小红书风格的 AI 工具推荐文案" | 符合平台风格的文案 |
| **标题优化** | "优化这个标题，提高点击率" | 生成 5 个爆款标题选项 |
| **素材搜集** | "找一些 AI 编程的高清图片" | 返回无版权图片链接 |
| **数据分析** | "分析我上周的公众号文章数据" | 阅读量/点赞/转发分析 |
| **粉丝互动** | "回复这条评论：'这个工具好用吗'" | 生成友好专业的回复 |

**价值**:
- ✍️ 内容创作效率提升 5 倍
- 📱 多平台一键分发
- 📊 数据驱动内容优化

---

## 4. 龙虾收费吗

### 4.1 开源版本（免费）

**OpenClaw 开源版**:
- ✅ **完全免费** - Apache 2.0 开源许可证
- ✅ **功能完整** - 核心功能全部开放
- ✅ **自行部署** - 需要自备服务器和 AI API Key
- ✅ **社区支持** - GitHub Issues + 社区论坛

**适用人群**:
- 有技术能力的个人开发者
- 愿意自行维护的企业 IT 部门
- 学习 AI 技术的学生

**成本构成**:
```
服务器成本：¥50-200/月（云服务器）
AI API 费用：¥100-500/月（按使用量）
时间成本：5-10 小时/月（维护更新）
```

### 4.2 商业版本（付费）

**CoPaw 商业版**:
- 💰 **订阅制** - ¥999/月起
- 🎯 **开箱即用** - 无需自行部署
- 🔧 **技术支持** - 专属客服 + 技术顾问
- 📚 **培训服务** - 在线课程 + 实战指导
- 🔒 **企业功能** - 权限管理 + 审计日志 + 数据备份

**适用人群**:
- 中小企业（快速部署需求）
- 非技术团队（零运维成本）
- 对稳定性要求高的企业

### 4.3 推荐方案

| 用户类型 | 推荐方案 | 月成本 |
|---------|---------|--------|
| **个人学习者** | 开源版 + 免费 AI 模型 | ¥50-100 |
| **个人开发者** | 开源版 + 付费 AI API | ¥200-500 |
| **小微企业** | CoPaw 基础版 | ¥999 |
| **中型企业** | CoPaw 专业版 + 定制技能 | ¥3000+ |
| **大型企业** | 私有化部署 + 定制开发 | 面议 |

---

## 5. OpenClaw 架构组成

### 5.1 整体架构图

```
┌─────────────────────────────────────────────────────────┐
│                    用户层 (User Layer)                    │
│  飞书 │ 钉钉 │ 企业微信 │ QQ │ 电报 │ Web Console       │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                  渠道适配层 (Channel Adapter)             │
│  消息接收 → 协议解析 → 格式统一 → 消息发送               │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   核心引擎层 (Core Engine)                │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │ 会话管理 │  │ 技能调度 │  │ 记忆系统 │              │
│  │ Session  │  │ Scheduler│  │ Memory   │              │
│  └──────────┘  └──────────┘  └──────────┘              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │ 提示词   │  │ 上下文   │  │ 安全审计 │              │
│  │ Prompt   │  │ Context  │  │ Auditor  │              │
│  └──────────┘  └──────────┘  └──────────┘              │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   技能执行层 (Skills Layer)               │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐           │
│  │Web 爬取│ │文件处理│ │数据分析│ │系统运维│           │
│  └────────┘ └────────┘ └────────┘ └────────┘           │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐           │
│  │邮件管理│ │日程管理│ │代码生成│ │安全扫描│           │
│  └────────┘ └────────┘ └────────┘ └────────┘           │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   AI 模型层 (Model Layer)                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │ OpenAI   │  │ Claude   │  │ 通义千问 │              │
│  │ GPT-5.4  │  │ Opus 4.6 │  │ Qwen 2.5 │              │
│  └──────────┘  └──────────┘  └──────────┘              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │ Gemini   │  │ 文心一言 │  │ 本地模型 │              │
│  │ 3.1 Pro  │  │ 4.0      │  │ Ollama   │              │
│  └──────────┘  └──────────┘  └──────────┘              │
└─────────────────────────────────────────────────────────┘
```

### 5.2 核心组件说明

#### 5.2.1 渠道适配层

**职责**: 统一不同聊天平台的协议差异

| 渠道 | 协议类型 | 支持功能 |
|------|---------|---------|
| **飞书** | HTTP Webhook | 文本/图片/文件/卡片消息 |
| **钉钉** | HTTP Webhook | 文本/Markdown/链接消息 |
| **企业微信** | HTTP API | 文本/图文/小程序卡片 |
| **QQ** | WebSocket | 文本/图片/语音 |
| **电报** | Bot API | 文本/文件/投票 |

#### 5.2.2 核心引擎层

**会话管理 (Session Manager)**:
- 维护用户会话状态
- 处理多轮对话上下文
- 会话超时自动清理

**技能调度 (Skill Scheduler)**:
- 根据用户意图匹配技能
- 并行执行多个技能
- 技能执行超时处理

**记忆系统 (Memory System)**:
- 短期记忆（会话上下文）
- 长期记忆（向量数据库）
- 记忆压缩与检索

**提示词引擎 (Prompt Engine)**:
- 动态提示词模板
-  Few-shot 示例注入
- 系统提示词优化

**安全审计 (Security Auditor)**:
- 敏感信息过滤
- 操作权限验证
- 审计日志记录

#### 5.2.3 技能执行层

**技能分类** (107+ 个技能):

| 分类 | 技能数量 | 代表技能 |
|------|---------|---------|
| Web/浏览器 | 18 个 | scrape, content-extractor, tech-stack-detector |
| DevOps/系统 | 20 个 | docker, systemd-manager, server-fleet-manager |
| 邮件/办公 | 8 个 | email-management, office-automation, docx, xlsx |
| 安全 | 8 个 | security-audit, vulnerability-scanner, clawsec |
| 数据/分析 | 10 个 | analyst, sql-toolkit, elasticsearch |
| 网络设备 | 6 个 | h3c-manager, cisco-manager, huawei-manager |
| 内容/媒体 | 8 个 | pptx, pdf, nano-pdf, xiaohongshu |
| AI/智能体 | 10 个 | agent-memory, self-improving-agent, dash-cog |
| 管理/产品 | 6 个 | cpo, product-manager, investor |
| 开发/测试 | 7 个 | developer, test-master, frontend, e2e-tester |
| 工具 | 6 个 | cron, weather, news, stock-watcher |

#### 5.2.4 AI 模型层

**支持的 AI 模型**:

| 厂商 | 模型 | 类型 | 适用场景 |
|------|------|------|---------|
| **OpenAI** | GPT-5.4 | 通用 | 代码生成、逻辑推理 |
| **Anthropic** | Claude Opus 4.6 | 通用 | 长文本分析、安全对话 |
| **Google** | Gemini 3.1 Pro | 多模态 | 图像理解、视频分析 |
| **阿里** | Qwen 2.5 Code | 代码专用 | 编程任务 |
| **百度** | 文心一言 4.0 | 通用 | 中文场景 |
| **本地** | Ollama (Llama3) | 通用 | 隐私敏感场景 |

---

## 6. 部署方式

### 6.1 部署方式对比

| 部署方式 | 难度 | 成本 | 适用场景 | 优点 | 缺点 |
|---------|------|------|---------|------|------|
| **本地部署** | ⭐⭐⭐ | 低 | 个人学习、数据敏感 | 数据自主、零月租 | 需自备服务器、自行维护 |
| **云端部署** | ⭐⭐ | 中 | 中小企业、快速上线 | 开箱即用、弹性扩展 | 月费成本、数据在云端 |
| **混合部署** | ⭐⭐⭐⭐ | 高 | 大型企业、合规要求 | 灵活配置、安全可控 | 架构复杂、运维成本高 |

### 6.2 本地部署（推荐个人用户）

#### 前置要求

- **操作系统**: Linux (Ubuntu 20.04+/CentOS 8+) / macOS / Windows (WSL2)
- **CPU**: 2 核 +
- **内存**: 4GB+ (推荐 8GB)
- **磁盘**: 20GB+ 可用空间
- **网络**: 可访问 GitHub 和 AI API

#### 安装步骤

```bash
# 1. 克隆仓库
git clone https://github.com/agentscope-ai/CoPaw.git
cd CoPaw

# 2. 创建 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate

# 3. 安装依赖
pip install -r requirements.txt

# 4. 配置环境变量
cp .env.example .env
# 编辑 .env 文件，填入 API Key

# 5. 启动服务
python -m copaw app --host 0.0.0.0 --port 8088

# 6. 访问控制台
# 浏览器打开 http://localhost:8088
```

#### 配置示例

```bash
# .env 配置文件
# AI 模型配置
OPENAI_API_KEY=sk-xxxxxxxxxxxxx
OPENAI_BASE_URL=https://api.openai.com/v1
OPENAI_MODEL=gpt-5.4

# 渠道配置
FEISHU_WEBHOOK_URL=https://open.feishu.cn/open-apis/bot/v2/hook/xxxxx
DINGTALK_ACCESS_TOKEN=xxxxxxxxxxxxx

# 数据库配置
DATABASE_URL=sqlite:///copaw.db

# 日志配置
LOG_LEVEL=INFO
```

### 6.3 云端部署（推荐企业用户）

#### CoPaw 云服务

**部署流程**:
1. 访问 https://copaw.ai 注册账号
2. 选择订阅方案（基础版/专业版/企业版）
3. 创建应用实例
4. 配置聊天渠道（飞书/钉钉/企业微信）
5. 启用所需技能
6. 开始使用

**优势**:
- ✅ 5 分钟快速上线
- ✅ 自动扩容，无需运维
- ✅ 数据自动备份
- ✅ 专业技术支持

**成本**:
- 基础版：¥999/月（10 用户）
- 专业版：¥2999/月（50 用户）
- 企业版：¥9999/月（不限用户）

### 6.4 Docker 部署（推荐开发者）

```bash
# 1. 拉取镜像
docker pull agentscope/copaw:latest

# 2. 创建配置文件
mkdir -p /opt/copaw/config
cp .env.example /opt/copaw/config/.env

# 3. 启动容器
docker run -d \
  --name copaw \
  -p 8088:8088 \
  -v /opt/copaw/config:/app/config \
  -v /opt/copaw/data:/app/data \
  agentscope/copaw:latest

# 4. 查看日志
docker logs -f copaw
```

---

## 7. 聊天渠道配置

### 7.1 飞书渠道（推荐企业用户）

#### 创建步骤

1. **登录飞书开放平台**
   - 访问 https://open.feishu.cn/
   - 使用企业管理员账号登录

2. **创建企业自建应用**
   - 进入「应用开发」→「企业自建应用」
   - 点击「创建应用」
   - 填写应用名称（如：AI 助手）
   - 上传应用图标（可选）

3. **配置机器人**
   - 进入「功能」→「机器人」
   - 点击「添加机器人」
   - 配置机器人名称和头像
   - 获取 Webhook URL

4. **配置权限**
   - 进入「权限管理」
   - 添加以下权限：
     - 发送消息
     - 读取消息
     - 用户信息读取

5. **发布应用**
   - 进入「版本管理与发布」
   - 点击「发布」
   - 等待审核（通常 1-2 个工作日）

6. **集成到 CoPaw**
   - 编辑 CoPaw 配置文件
   - 填入飞书 Webhook URL
   - 重启 CoPaw 服务

#### 配置示例

```json
{
  "channel": "feishu",
  "enabled": true,
  "webhook_url": "https://open.feishu.cn/open-apis/bot/v2/hook/xxxxxxxxxxxxx",
  "app_id": "cli_xxxxxxxxxxxxx",
  "app_secret": "xxxxxxxxxxxxx",
  "verification_token": "xxxxxxxxxxxxx"
}
```

### 7.2 钉钉渠道

#### 创建步骤

1. **登录钉钉开放平台**
   - 访问 https://open.dingtalk.com/
   - 使用企业管理员账号登录

2. **创建企业内部应用**
   - 进入「应用开发」→「企业内部应用」
   - 点击「创建应用」
   - 填写应用信息

3. **配置机器人**
   - 进入「机器人」功能
   - 创建机器人
   - 获取 Access Token

4. **配置权限**
   - 添加「机器人消息」权限
   - 添加「通讯录」权限（可选）

5. **集成到 CoPaw**
   - 配置钉钉 Access Token
   - 测试消息发送

#### 配置示例

```json
{
  "channel": "dingtalk",
  "enabled": true,
  "app_key": "xxxxxxxxxxxxx",
  "app_secret": "xxxxxxxxxxxxx",
  "agent_id": "xxxxxxxxxxxxx"
}
```

### 7.3 企业微信渠道

#### 创建步骤

1. **登录企业微信管理后台**
   - 访问 https://work.weixin.qq.com/
   - 使用企业管理员账号登录

2. **创建自建应用**
   - 进入「应用管理」→「应用」
   - 点击「创建应用」
   - 填写应用信息

3. **配置 API 接收消息**
   - 进入「接收消息」配置
   - 填写 URL、Token、EncodingAESKey
   - 验证配置

4. **获取凭证**
   - 记录 CorpID、Secret、AgentID

5. **集成到 CoPaw**
   - 配置企业微信凭证
   - 测试消息收发

#### 配置示例

```json
{
  "channel": "wecom",
  "enabled": true,
  "corp_id": "xxxxxxxxxxxxx",
  "corp_secret": "xxxxxxxxxxxxx",
  "agent_id": "xxxxxxxxxxxxx",
  "token": "xxxxxxxxxxxxx",
  "encoding_aes_key": "xxxxxxxxxxxxx"
}
```

### 7.4 QQ 机器人渠道

#### 使用方案

**方案一：Go-CQHTTP**（推荐）
```bash
# 1. 下载 Go-CQHTTP
wget https://github.com/Mrs4s/go-cqhttp/releases/latest/download/go-cqhttp_linux_amd64.tar.gz

# 2. 解压配置
tar -xzf go-cqhttp_linux_amd64.tar.gz
./go-cqhttp -c config.yml

# 3. 配置正向 WebSocket
# 编辑 config.yml，配置 WebSocket 服务器地址

# 4. 集成到 CoPaw
# CoPaw 通过 WebSocket 连接 Go-CQHTTP
```

**方案二：OneBot 协议**
- 使用支持 OneBot 协议的 QQ 机器人框架
- CoPaw 通过 HTTP API 调用

### 7.5 电报渠道

#### 创建步骤

1. **联系 @BotFather**
   - 在 Telegram 搜索 @BotFather
   - 发送 `/newbot` 创建新机器人
   - 设置机器人名称和用户名

2. **获取 Token**
   - BotFather 会返回 Bot Token
   - 格式：`123456789:ABCdefGHIjklMNOpqrsTUVwxyz`

3. **配置 CoPaw**
   - 填入 Bot Token
   - 配置 Webhook（可选）

#### 配置示例

```json
{
  "channel": "telegram",
  "enabled": true,
  "bot_token": "123456789:ABCdefGHIjklMNOpqrsTUVwxyz",
  "webhook_url": "https://your-domain.com/telegram/webhook"
}
```

---

## 8. 模型配置

### 8.1 对接国内模型

#### 通义千问（推荐）

**申请 API Key**:
1. 访问 https://dashscope.console.aliyun.com/
2. 注册/登录阿里云账号
3. 开通「通义千问」服务
4. 创建 API Key

**配置示例**:
```bash
# .env 文件
DASHSCOPE_API_KEY=sk-xxxxxxxxxxxxx
DASHSCOPE_MODEL=qwen-max
DASHSCOPE_BASE_URL=https://dashscope.aliyuncs.com/api/v1
```

**Python 调用示例**:
```python
from dashscope import Generation

response = Generation.call(
    model='qwen-max',
    prompt='你好，请介绍一下自己'
)
print(response.output.text)
```

#### 文心一言

**申请 API Key**:
1. 访问 https://cloud.baidu.com/product/wenxinworkshop
2. 注册/登录百度账号
3. 创建应用获取 API Key

**配置示例**:
```bash
# .env 文件
QIANFAN_ACCESS_KEY=xxxxxxxxxxxxx
QIANFAN_SECRET_KEY=xxxxxxxxxxxxx
QIANFAN_MODEL=ERNIE-Bot-4.0
```

#### 讯飞星火

**申请 API Key**:
1. 访问 https://www.xfyun.cn/service/spark
2. 注册/登录讯飞账号
3. 创建应用获取 API Key 和 Secret

**配置示例**:
```bash
# .env 文件
IFLYTEK_APP_ID=xxxxxxxxxxxxx
IFLYTEK_API_KEY=xxxxxxxxxxxxx
IFLYTEK_API_SECRET=xxxxxxxxxxxxx
IFLYTEK_MODEL=spark-v3.5
```

### 8.2 对接国际模型

#### OpenAI GPT

**申请 API Key**:
1. 访问 https://platform.openai.com/
2. 注册账号（需要海外手机号）
3. 充值账户（最低$5）
4. 创建 API Key

**配置示例**:
```bash
# .env 文件
OPENAI_API_KEY=sk-xxxxxxxxxxxxx
OPENAI_MODEL=gpt-5.4
OPENAI_BASE_URL=https://api.openai.com/v1
```

#### Anthropic Claude

**申请 API Key**:
1. 访问 https://console.anthropic.com/
2. 注册账号
3. 创建 API Key

**配置示例**:
```bash
# .env 文件
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxxx
ANTHROPIC_MODEL=claude-opus-4.6
```

### 8.3 本地模型（隐私保护）

#### Ollama 部署

```bash
# 1. 安装 Ollama
curl -fsSL https://ollama.ai/install.sh | sh

# 2. 下载模型
ollama pull llama3:8b

# 3. 启动服务
ollama serve

# 4. CoPaw 配置
# .env 文件
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=llama3:8b
```

**优势**:
- ✅ 数据完全本地，隐私保护
- ✅ 零 API 费用
- ✅ 离线可用

**劣势**:
- ❌ 模型效果不如云端大模型
- ❌ 需要本地 GPU（推荐）
- ❌ 响应速度较慢

### 8.4 模型选择建议

| 场景 | 推荐模型 | 理由 |
|------|---------|------|
| **代码生成** | GPT-5.4 / Qwen 2.5 Code | 代码能力强，准确率高 |
| **中文对话** | 通义千问 / 文心一言 | 中文理解更好 |
| **长文本分析** | Claude Opus 4.6 | 200K 上下文窗口 |
| **多模态** | Gemini 3.1 Pro | 图像/视频理解强 |
| **隐私敏感** | Ollama (Llama3) | 本地部署，数据不出域 |
| **成本敏感** | 通义千问 / 本地模型 | 性价比高 |

---

## 📚 参考资源

### 官方文档
- [OpenClaw 官网](https://cmdop.com/)
- [CoPaw 官方仓库](https://github.com/agentscope-ai/CoPaw)
- [CoPaw 文档](https://copaw.ai/docs)

### 渠道平台
- [飞书开放平台](https://open.feishu.cn/)
- [钉钉开放平台](https://open.dingtalk.com/)
- [企业微信开放平台](https://work.weixin.qq.com/)
- [Telegram Bot API](https://core.telegram.org/bots/api)

### AI 模型平台
- [通义千问](https://dashscope.console.aliyun.com/)
- [文心一言](https://cloud.baidu.com/product/wenxinworkshop)
- [讯飞星火](https://www.xfyun.cn/service/spark)
- [OpenAI](https://platform.openai.com/)
- [Anthropic](https://console.anthropic.com/)
- [Ollama](https://ollama.ai/)

---

## 💡 常见问题

### Q1: 龙虾机器人需要编程基础吗？
**A**: 不需要！龙虾机器人设计为零门槛，通过聊天工具（如飞书、微信）直接对话即可使用。只有自定义技能开发才需要编程基础。

### Q2: 数据安全性如何保障？
**A**: 
- 本地部署：数据完全自主，存储在本地服务器
- 云端部署：采用 HTTPS 加密传输，支持数据备份和权限管理
- 敏感信息：支持敏感词过滤和操作审计日志

### Q3: 一个账号可以绑定多少个聊天渠道？
**A**: 理论上无限制。实际使用中，建议每个渠道创建一个机器人实例，便于管理和权限控制。

### Q4: Skills 技能可以自己开发吗？
**A**: 可以！CoPaw 提供 Skills 开发框架，支持 Python 编写自定义技能。参考官方文档：https://copaw.ai/docs/skills-development

### Q5: 支持私有化部署吗？
**A**: 支持！OpenClaw 开源版可完全私有化部署。企业版提供私有化部署服务和技术支持。

---

**文档版本**: v1.0  
**最后更新**: 2026-03-22  
**维护者**: hjs2015  
**许可证**: CC BY-SA 4.0
