# 老男孩 AI 编程实战第一期 - 完整教程内容

> **来源**: 飞书云文档 https://my.feishu.cn/wiki/AlBuwnaeTidXVOkT96gcuavrn8b  
> **最新修改**: 2026-03-22  
> **提取时间**: 2026-03-22 11:55

---

## 📑 完整目录（37 个章节）

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

## 📖 核心内容详解

### 3.3 提示词（Prompt）

**定义**: 提示词就是发给 AI 大模型的精准编程指令，说白了就是你对 AI 提出的具体需求，也是 AI 编程里最核心的操作。

**编写原则**:
- ✅ 不能太笼统，越具体越好用
- ✅ 完整清晰的需求就是标准提示词
- ✅ 指令越明确，AI 给出的代码结果越精准

**优秀示例**:
```
帮我排查这段 Java 代码的空指针异常，保留原有业务逻辑，逐行添加易懂的中文注释
```

**好处**: 省去反复修改的麻烦

---

### 3.4 上下文长度（Context Length）

**定义**: 上下文长度可以直接理解为 AI 大模型的短期记忆力上限，计量单位就是 Token，代表模型能一次性完整记住、连贯处理的所有前置内容总量。

**编程场景应用**:
- 粘贴一整段长代码让 AI 逐行分析优化
- 多轮对话的连续编程需求

**问题**: 上下文长度太短 → AI 会"断片儿"，只能处理后半段

**优势**: 上下文长度越长 → AI 越能承接整段长代码，全程逻辑连贯不脱节

---

### 3.5 Skills（技能）

**定义**: Skills 可以直白理解为给 AI 大模型定制的专项能力插件包，是 AI 完成精准编程任务的核心专属技能，并非模型自带的泛化能力，而是针对性配置的专业功能模块。

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

---

### 3.6 MCP（模型上下文协议）

**全称**: Model Context Protocol（模型上下文协议）

**定义**: 是 AI 编程与大模型应用里的通用连接标准，可以通俗理解为 AI 世界的"USB-C 统一接口"。

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

### 第 2 章 龙虾机器人介绍

#### 1.龙虾的由来

**品牌演变历史**:

| 阶段 | 名称 | 原因 |
|------|------|------|
| **最初** | Clawdbot | 原始名称 |
| **第一次改名** | Moltbot | 因为 Clawd 的发音和 A 社的 Claude 发音很相似（都叫克劳德），被 A 社盯上，避免版权纠纷 |
| **最终名称** | OpenClaw | 仅过了三天又改名 |

**品牌寓意**:
- **Claw** = 爪子或者龙虾的鳌 🦞
- **选择龙虾的原因**: 作者的家乡盛产龙虾，算是给家乡代言了

---

#### 2.龙虾为什么这么火

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

---

### AI 编程产品分类对比表

| 大类分类 | 核心工具 | 核心特点 | 适用场景 |
|---------|---------|---------|---------|
| **Chat 聊天型** | OpenAI: ChatGPT<br>Anthropic: Claude<br>Google: Gemini | 自然语言对话<br>无专属编程环境<br>轻量化问答<br>零门槛 | 代码咨询<br>片段生成<br>Bug 排查<br>思路梳理 |
| **IDE 集成型** | Kiro<br>Cursor<br>Antigravity | 原生 AI IDE<br>沉浸式编码<br>实时补全、调试<br>项目级辅助 | 专业项目开发<br>日常编码<br>全栈工程编写 |
| **CLI 命令行型** | OpenAI：Codex<br>Anthropic：Claude Code | 纯终端交互<br>无图形界面<br>高效批量处理<br>自动化运维 | 服务器开发<br>命令行批量操作<br>自动化部署 |

---

### AI 编程主流模型

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

---

### 龙虾机器人应用场景

#### 3.1 普通人：零门槛私人数字管家
- 日常任务管理
- 信息查询助手
- 个人日程安排

#### 3.2 IT 从业者：技术流程效率工具
- 代码生成与审查
- 自动化脚本编写
- 技术文档生成

#### 3.3 企业：轻量化办公自动化助手
- 工作流程自动化
- 数据报表生成
- 客户服务响应

#### 3.4 自媒体：内容运营提速工具
- 内容创意生成
- 文案撰写辅助
- 多平台内容分发

---

## 💡 核心概念总结

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

### Skills vs MCP 关系图解

```
┌─────────────────────────────────────────────┐
│           AI 大模型                          │
│  ┌─────────────────────────────────────┐    │
│  │  Skills（专项能力插件包）             │    │
│  │  • 代码生成 Skill                    │    │
│  │  • Bug 排查 Skill                    │    │
│  │  • SQL 编写 Skill                    │    │
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

---

## 📊 学习路径建议

### 新手入门（第 1 周）
1. 理解 AI 编程基本概念（提示词、Token、上下文）
2. 了解主流 AI 编程工具分类
3. 注册并体验 Chat 聊天型 AI

### 进阶提升（第 2-3 周）
1. 学习提示词编写技巧
2. 掌握 IDE 集成型工具使用
3. 理解 Skills 和 MCP 的作用

### 实战应用（第 4 周起）
1. 部署龙虾机器人
2. 配置聊天渠道
3. 对接 AI 模型
4. 开发实际应用场景

---

## 🔗 快速跳转链接

### 第 1 章 基础概念
- [AI 编程产品分类](#LfLLdWN2BoAPk3xDuJScHSJQnQ2)
- [AI 编程主流模型](#VWVsd7Z5ooDr7nxPWKtcHFrpnfe)
- [提示词](#PteAd2BlToec3IxiWkVcXDs5nhh)
- [上下文长度](#HC2KdQwPAoPAhXx1wWvceWUCnSc)
- [Skills](#XTiedNb70oKo0xxTX37cf3iinid)
- [MCP](#BrBZdVldlo8gGqx6bmBcZWpBnlf)

### 第 2 章 龙虾介绍
- [龙虾的由来](#KToWdFeZToFUF0xJnrqcfbTTnFg)
- [为什么这么火](#GjlYdsPoIoVSoSxO1GPcP3A7ns2)
- [应用场景](#OYM0dx53FocF66xJpYicnAOCnOc)

### 第 3-6 章 实战部署
- [架构说明](#HzwcdvOkkoKCvlxno1vcxE8unOc)
- [安装部署](#CCjXdTA3wopHswx4lRZcYVCTnSe)
- [渠道配置](#VgrndQpPao06ZPxNzGnc1YYbnzd)
- [模型对接](#OK0fd2vAHoHBEkxP6wAcfKZpnbc)

---

**文档整理时间**: 2026-03-22 11:55  
**来源**: 飞书云文档 - 老男孩 AI 编程实战第一期  
**整理者**: hjs2015  
**文档版本**: v2.0（完整版）
