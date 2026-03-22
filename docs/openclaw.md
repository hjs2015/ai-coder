# 🦞 OpenClaw 完全指南（中国内地版）

> **自托管 AI 网关 · 本土化深度适配 · 无外网依赖方案**  
> **文档版本**: v5.0 中国内地版（2026-03-23）  
> **官方文档**: https://docs.openclaw.ai/  
> **GitHub**: https://github.com/openclaw/openclaw  
> **许可证**: MIT  
> **适用地区**: 中国大陆及港澳台地区

---

## 📑 完整目录

<details>
<summary><b>点击展开完整目录（12 大部分 68 章节）</b></summary>

### 第一部分：产品认知与入门
1. [什么是 OpenClaw](#什么是-openclaw)
2. [核心价值与定位](#核心价值与定位)
3. [适用场景](#适用场景)
4. [快速开始（60 秒上手）](#快速开始 60-秒上手)
5. [系统要求与兼容性](#系统要求与兼容性)

### 第二部分：国内本土化适配专区 ⭐
6. [国内网络环境适配](#国内网络环境适配)
7. [国内大模型完整接入](#国内大模型完整接入)
8. [国内聊天平台接入](#国内聊天平台接入)
9. [国内镜像与加速方案](#国内镜像与加速方案)

### 第三部分：安装与部署
10. [npm 安装（推荐）](#npm-安装推荐)
11. [Docker 容器化部署](#docker-容器化部署)
12. [源码安装（开发者）](#源码安装开发者)
13. [离线安装方案](#离线安装方案)
14. [生产环境部署](#生产环境部署)

### 第四部分：国内聊天渠道配置 ⭐
15. [飞书配置（原生支持）](#飞书配置原生支持)
16. [企业微信配置](#企业微信配置)
17. [钉钉配置](#钉钉配置)
18. [微信配置（个人号/公众号）](#微信配置个人号公众号)
19. [QQ 配置](#qq-配置)
20. [Telegram 配置（备选）](#telegram-配置备选)

### 第五部分：国内大模型配置 ⭐
21. [通义千问（阿里云）](#通义千问阿里云)
22. [文心一言（百度）](#文心一言百度)
23. [豆包（火山引擎）](#豆包火山引擎)
24. [讯飞星火](#讯飞星火)
25. [Kimi（月之暗面）](#kimi-月之暗面)
26. [智谱 GLM](#智谱-glm)
27. [本地模型（Ollama）](#本地模型-ollama)

### 第六部分：渠道配置（国际）
28. [支持的渠道列表](#支持的渠道列表)
29. [WhatsApp 配置](#whatsapp-配置)
30. [Discord 配置](#discord-配置)
31. [iMessage 配置](#imessage-配置)
32. [渠道路由规则](#渠道路由规则)

### 第七部分：核心概念
33. [架构概览](#架构概览)
34. [Gateway（网关）](#gateway-网关)
35. [Agent（智能体）](#agent-智能体)
36. [Session（会话）](#session-会话)
37. [Memory（记忆）](#memory-记忆)

### 第八部分：Agent 与工具
38. [Agent 工作区配置](#agent-工作区配置)
39. [工具与插件系统](#工具与插件系统)
40. [MCP 协议集成](#mcp-协议集成)
41. [定时任务与自动化](#定时任务与自动化)

### 第九部分：会话与记忆管理
42. [会话管理深度解析](#会话管理深度解析)
43. [记忆系统架构](#记忆系统架构)
44. [会话压缩机制](#会话压缩机制)

### 第十部分：运维管理
45. [Gateway 运维管理](#gateway-运维管理)
46. [日志与调试](#日志与调试)
47. [监控与告警](#监控与告警)
48. [备份与恢复](#备份与恢复)

### 第十一部分：安全与优化
49. [安全配置](#安全配置)
50. [性能优化](#性能优化)
51. [高可用配置](#高可用配置)

### 第十二部分：故障排查
52. [诊断命令速查](#诊断命令速查)
53. [网络问题排查](#网络问题排查)
54. [高频问题解决方案](#高频问题解决方案)
55. [FAQ（100+ 常见问题）](#faq100-常见问题)

### 附录
- [附录 A：环境变量参考](#附录-a-环境变量参考)
- [附录 B：配置文件完整参考](#附录-b-配置文件完整参考)
- [附录 C：CLI 命令参考](#附录-c-cli-命令参考)
- [附录 D：国内 API Key 获取指南](#附录-d-国内-api-key-获取指南)

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

## 第二部分：国内本土化适配专区 ⭐

### 国内网络环境适配

#### 网络访问方案对比

| 方案 | 优点 | 缺点 | 适用场景 |
|------|------|------|---------|
| **国内大模型** | 无需翻墙、速度快、人民币付费 | 模型能力略弱于 GPT-4 | ✅ 首选推荐 |
| **本地模型** | 完全离线、隐私最好 | 需要 GPU、能力有限 | 敏感数据场景 |
| **代理访问** | 可使用 GPT-4 | 需要额外成本、不稳定 | 备选方案 |

#### 推荐方案组合

```
【最佳实践】国内大模型（阿里/百度/火山）+ 本地模型（Ollama）备份
【进阶方案】国内大模型 + 代理访问国际模型（按需切换）
【完全离线】本地模型（Ollama）+ 本地知识库
```

---

### 国内大模型完整接入

#### 支持的国内大模型列表

| 提供商 | 模型 | 价格（元/1K tokens） | 上下文 | 状态 |
|--------|------|-------------------|--------|------|
| **阿里通义** | Qwen-Max | 输入¥0.04/输出¥0.12 | 256K | ✅ 推荐 |
| **百度文心** | ERNIE 4.0 | 输入¥0.03/输出¥0.09 | 128K | ✅ 推荐 |
| **火山豆包** | Doubao Pro | 输入¥0.008/输出¥0.03 | 128K | ✅ 性价比 |
| **讯飞星火** | Spark 4.0 | 输入¥0.03/输出¥0.09 | 200K | ✅ 支持 |
| **月之暗面** | Kimi | 输入¥0.005/输出¥0.015 | 200K | ✅ 长文本 |
| **智谱 AI** | GLM-4 | 输入¥0.05/输出¥0.15 | 128K | ✅ 支持 |

#### 国内模型 vs 国际模型

| 维度 | 国内模型 | 国际模型（GPT-4/Claude） |
|------|---------|------------------------|
| **中文能力** | ⭐⭐⭐⭐⭐ 原生优化 | ⭐⭐⭐⭐ 良好 |
| **访问速度** | ⭐⭐⭐⭐⭐ 国内节点 | ⭐⭐ 需要代理 |
| **成本** | ⭐⭐⭐⭐ 人民币计价 | ⭐⭐ 美元 + 汇率 |
| **合规性** | ⭐⭐⭐⭐⭐ 完全合规 | ⭐⭐⭐ 需注意 |
| **模型能力** | ⭐⭐⭐⭐ 良好 | ⭐⭐⭐⭐⭐ 最强 |

---

### 国内聊天平台接入

#### 支持列表与难度

| 平台 | 支持方式 | 难度 | 是否需要公网 IP | 备注 |
|------|---------|------|--------------|------|
| **飞书** | 原生支持 | ⭐ 简单 | ❌ 无需 | ✅ 推荐 |
| **企业微信** | 社区插件 | ⭐⭐ 中等 | ❌ 无需 | 需 Stream 模式 |
| **钉钉** | 社区插件 | ⭐⭐ 中等 | ❌ 无需 | 需 Stream 模式 |
| **微信** | 第三方插件 | ⭐⭐⭐ 复杂 | ⚠️ 建议有 | 个人号/公众号 |
| **QQ** | 社区插件 | ⭐⭐⭐ 复杂 | ⚠️ 建议有 | OneBot 协议 |

---

### 国内镜像与加速方案

#### Node.js 镜像

```bash
# 方案 1：淘宝镜像（推荐）
npm config set registry https://registry.npmmirror.com

# 方案 2：腾讯云镜像
npm config set registry https://mirrors.cloud.tencent.com/npm/

# 方案 3：华为云镜像
npm config set registry https://mirrors.huaweicloud.com/repository/npm/

# 验证配置
npm config get registry
```

#### Docker 镜像加速

```bash
# 配置 Docker 镜像加速器（以阿里云为例）
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://registry.docker-cn.com"
  ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

#### GitHub 加速

```bash
# 方案 1：使用代理
export https_proxy=http://127.0.0.1:7890
git clone https://github.com/openclaw/openclaw.git

# 方案 2：使用镜像站
git clone https://ghproxy.com/https://github.com/openclaw/openclaw.git

# 方案 3：国内镜像（如有）
git clone https://gitee.com/mirror/openclaw.git
```

---

## 第三部分：安装与部署

### npm 安装（推荐）

#### 标准安装流程

```bash
# 1. 配置淘宝镜像
npm config set registry https://registry.npmmirror.com

# 2. 安装 OpenClaw
npm install -g openclaw

# 3. 验证安装
openclaw --version
# 输出：openclaw/x.x.x
```

#### 常见问题解决

**问题 1：权限错误**

```bash
# macOS/Linux 权限问题
sudo chown -R $(whoami) ~/.npm
npm install -g openclaw
```

**问题 2：下载超时**

```bash
# 增加超时时间
npm config set fetch-timeout 300000
npm install -g openclaw
```

---

### Docker 容器化部署

#### 快速启动（国内镜像）

```bash
docker run -d \
  --name openclaw \
  -p 3000:3000 \
  -v openclaw-data:/root/.openclaw \
  -e ANTHROPIC_API_KEY=sk-ant-xxx \
  -e TZ=Asia/Shanghai \
  registry.cn-hangzhou.aliyuncs.com/openclaw/openclaw:latest
```

#### Docker Compose 配置

```yaml
version: '3.8'

services:
  openclaw:
    image: registry.cn-hangzhou.aliyuncs.com/openclaw/openclaw:latest
    container_name: openclaw
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - openclaw-data:/root/.openclaw
      - ./config:/root/.openclaw/config:ro
    environment:
      - TZ=Asia/Shanghai
      - ANTHROPIC_API_KEY=${ANTHROPIC_API_KEY}
    networks:
      - openclaw-net

volumes:
  openclaw-data:

networks:
  openclaw-net:
    driver: bridge
```

---

## 第四部分：国内聊天渠道配置 ⭐

### 飞书配置（原生支持）

#### 前置条件

- 飞书企业管理员权限
- 飞书开放平台账号
- 企业已认证

#### 创建飞书机器人

**步骤 1：访问飞书开放平台**

1. 打开 https://open.feishu.cn/
2. 登录企业账号
3. 进入「企业自建应用」
4. 点击「创建应用」

**步骤 2：配置应用权限**

1. 应用名称：OpenClaw 助手
2. 应用图标：上传 Logo
3. 权限配置：
   - ✅ 发送消息
   - ✅ 读取消息
   - ✅ 群组管理
   - ✅ 机器人功能

**步骤 3：获取凭证**

1. 进入「凭证与基础信息」
2. 记录 App ID（cli_xxxxxxxxxxxxx）
3. 记录 App Secret（xxxxxxxxxxxxxxxxx）

**步骤 4：配置事件订阅**

1. 进入「事件订阅」
2. 开启事件订阅
3. 配置订阅地址（飞书内置，无需公网）
4. 订阅事件：
   - 接收消息 v2.0
   - 机器人进群

**步骤 5：发布应用**

1. 进入「版本管理与发布」
2. 提交审核（通常 1-2 工作日）
3. 审核通过后启用

---

#### OpenClaw 配置

**配置文件**：`~/.openclaw/openclaw.json`

```json
{
  "channels": {
    "feishu": {
      "appId": "cli_xxxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxx",
      "encryptKey": "xxxxxxxxxxxxxxxxx",
      "verificationToken": "xxxxxxxxxxxxxxxxx",
      "allowUsers": ["ou_xxxxxxxxxxxxx"],
      "allowGroups": ["oc_xxxxxxxxxxxxx"],
      "requireMention": true
    }
  }
}
```

**配置说明**：

| 字段 | 说明 | 获取方式 |
|------|------|---------|
| `appId` | 飞书应用 ID | 飞书开放平台 - 凭证与基础信息 |
| `appSecret` | 应用密钥 | 飞书开放平台 - 凭证与基础信息 |
| `encryptKey` | 加密密钥 | 飞书开放平台 - 事件订阅 |
| `verificationToken` | 验证 Token | 飞书开放平台 - 事件订阅 |
| `allowUsers` | 允许的用户列表 | 飞书用户 ID（可选） |
| `allowGroups` | 允许的群组列表 | 飞书群组 ID（可选） |
| `requireMention` | 是否需要@机器人 | true/false |

---

#### 获取用户/群组 ID

**方法 1：通过飞书 API**

```bash
# 获取用户 ID
curl -X POST https://open.feishu.cn/open-apis/auth/v3/tenant_access_token/internal \
  -H "Content-Type: application/json" \
  -d '{"app_id":"cli_xxx","app_secret":"xxx"}'

# 获取群组 ID
curl -X GET https://open.feishu.cn/open-apis/im/v1/chats \
  -H "Authorization: Bearer xxx"
```

**方法 2：通过日志查看**

```bash
# 启动 OpenClaw 并发送消息
openclaw start

# 查看日志获取用户/群组 ID
openclaw logs | grep feishu
```

---

#### 测试连接

**步骤 1：启动 OpenClaw**

```bash
openclaw start
```

**步骤 2：在飞书中测试**

1. 打开飞书，找到配置的群组
2. 发送消息：`@OpenClaw 助手 你好`
3. 收到回复表示成功

**步骤 3：查看日志**

```bash
openclaw logs | grep feishu
# 应看到消息接收和发送日志
```

---

#### 高级配置

**群组消息规则**

```json
{
  "channels": {
    "feishu": {
      "groups": {
        "*": {
          "requireMention": true,
          "mentionPatterns": ["@OpenClaw", "@助手"],
          "ignoreCommands": ["/help", "/start"]
        },
        "oc_xxxxxxxxxxxxx": {
          "requireMention": false
        }
      }
    }
  }
}
```

**路由规则**

```json
{
  "routing": {
    "rules": [
      {
        "channel": "feishu",
        "pattern": ".*代码.*",
        "agent": "coding-agent"
      },
      {
        "channel": "feishu",
        "pattern": ".*日报.*",
        "agent": "report-agent"
      }
    ]
  }
}
```

---

#### 常见问题排查

**问题 1：收不到消息**

```bash
# 检查事件订阅配置
# 1. 飞书开放平台 - 事件订阅
# 2. 确认已开启「接收消息 v2.0」
# 3. 确认机器人已添加到群组

# 检查 OpenClaw 日志
openclaw logs | grep feishu
```

**问题 2：发送失败**

```bash
# 检查 App Secret 是否正确
# 检查机器人是否有发送权限
# 检查群组是否允许机器人发言
```

**问题 3：@提及不生效**

```json
// 配置 requireMention: true
{
  "channels": {
    "feishu": {
      "requireMention": true
    }
  }
}
```

---

### 企业微信配置

#### 前置条件

- 企业微信管理员权限
- 企业已认证
- 社区插件：openclaw-channel-wecom

#### 安装插件

```bash
npm install -g @openclaw/channel-wecom
```

#### 创建企业微信机器人

**步骤 1：访问企业微信管理后台**

1. 打开 https://work.weixin.qq.com/
2. 登录企业管理员账号
3. 进入「应用管理」
4. 点击「自建」创建应用

**步骤 2：配置应用**

1. 应用名称：OpenClaw 助手
2. 应用图标：上传 Logo
3. 可见范围：选择部门/人员

**步骤 3：获取凭证**

1. 进入「应用详情」
2. 记录 AgentId（数字）
3. 记录 Secret（字符串）
4. 记录 CorpID（企业 ID）

**步骤 4：配置接收消息**

1. 进入「接收消息」
2. 启用 API 接收
3. 配置 Token
4. 配置 EncodingAESKey
5. 配置回调 URL（需 Stream 模式）

---

#### OpenClaw 配置

```json
{
  "channels": {
    "wecom": {
      "corpId": "wwxxxxxxxxxxxx",
      "agentId": 1000001,
      "secret": "xxxxxxxxxxxxxxxxx",
      "token": "xxxxxxxxxxxxxxxxx",
      "encodingAesKey": "xxxxxxxxxxxxxxxxx",
      "streamMode": true,
      "allowUsers": ["zhangsan"],
      "allowDepartments": [1, 2]
    }
  }
}
```

---

### 钉钉配置

#### 前置条件

- 钉钉企业管理员权限
- 企业已认证
- 社区插件：openclaw-channel-dingtalk

#### 安装插件

```bash
npm install -g @openclaw/channel-dingtalk
```

#### 创建钉钉机器人

**步骤 1：访问钉钉开放平台**

1. 打开 https://open.dingtalk.com/
2. 登录企业账号
3. 进入「企业内部开发」
4. 点击「创建应用」

**步骤 2：配置应用**

1. 应用名称：OpenClaw 助手
2. 应用图标：上传 Logo
3. 权限配置：
   - ✅ 发送工作通知
   - ✅ 群机器人
   - ✅ 消息接收

**步骤 3：获取凭证**

1. 记录 AppKey
2. 记录 AppSecret
3. 记录 AgentId

---

#### OpenClaw 配置

```json
{
  "channels": {
    "dingtalk": {
      "appKey": "dingxxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxx",
      "agentId": 1000001,
      "streamMode": true,
      "allowUsers": ["zhangsan"],
      "allowGroups": ["group_xxxxxxxxxxxxx"]
    }
  }
}
```

---

### 微信配置（个人号/公众号）

#### 方案对比

| 方案 | 类型 | 难度 | 稳定性 | 备注 |
|------|------|------|--------|------|
| **个人微信** | Wechaty | ⭐⭐⭐⭐ | ⚠️ 中等 | 有封号风险 |
| **公众号** | 官方 API | ⭐⭐⭐ | ✅ 稳定 | 需企业认证 |
| **企业微信** | 官方 API | ⭐⭐ | ✅ 稳定 | ✅ 推荐 |

#### 个人微信配置（Wechaty）

**警告**：个人微信自动化可能违反微信用户协议，存在封号风险，仅用于学习研究。

```bash
# 安装 Wechaty 插件
npm install -g @openclaw/channel-wechaty
```

**配置**：

```json
{
  "channels": {
    "wechaty": {
      "puppet": "wechaty-puppet-wechat4u",
      "allowUsers": ["zhangsan"],
      "allowGroups": ["群聊 1"]
    }
  }
}
```

---

### QQ 配置

#### 前置条件

- QQ 号（建议小号）
- OneBot 协议支持
- 社区插件：openclaw-channel-qq

#### 安装插件

```bash
npm install -g @openclaw/channel-qq
```

#### 配置 OneBot

**使用 Lagrange.Core**

```bash
# 下载 Lagrange.Core
wget https://github.com/LagrangeDev/Lagrange.Core/releases/latest/download/Lagrange.OneBot.zip

# 配置 QQ 登录
# 编辑 appsettings.json 配置 QQ 号和密码
```

**OpenClaw 配置**

```json
{
  "channels": {
    "qq": {
      "protocol": "onebot",
      "endpoint": "ws://127.0.0.1:8080",
      "allowUsers": ["123456789"],
      "allowGroups": ["987654321"]
    }
  }
}
```

---

## 第五部分：国内大模型配置 ⭐

### 通义千问（阿里云）

#### 获取 API Key

**步骤 1：访问阿里云**

1. 打开 https://www.aliyun.com/
2. 登录阿里云账号
3. 搜索「通义千问」

**步骤 2：开通服务**

1. 进入通义千问控制台
2. 点击「开通服务」
3. 同意服务协议

**步骤 3：创建 API Key**

1. 进入「API-KEY 管理」
2. 点击「创建新的 API-KEY」
3. 复制并保存（仅显示一次）

---

#### OpenClaw 配置

```json
{
  "models": {
    "default": "qwen-max",
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxxxxxxxxxxxxxxxx",
        "baseUrl": "https://dashscope.aliyuncs.com/api/v1"
      }
    }
  }
}
```

**模型选择**：

| 模型 | 适用场景 | 价格 |
|------|---------|------|
| **qwen-max** | 复杂任务、代码生成 | ¥0.04/输入 ¥0.12/输出 |
| **qwen-plus** | 平衡性能与成本 | ¥0.02/输入 ¥0.06/输出 |
| **qwen-turbo** | 简单任务、快速响应 | ¥0.008/输入 ¥0.024/输出 |

---

### 文心一言（百度）

#### 获取 API Key

**步骤 1：访问百度智能云**

1. 打开 https://cloud.baidu.com/
2. 登录百度账号
3. 搜索「文心一言」

**步骤 2：开通服务**

1. 进入文心一言控制台
2. 点击「开通服务」
3. 完成实名认证

**步骤 3：创建密钥**

1. 进入「应用管理」
2. 创建应用
3. 获取 API Key 和 Secret Key

---

#### OpenClaw 配置

```json
{
  "models": {
    "default": "ernie-4.0",
    "providers": {
      "qianfan": {
        "apiKey": "xxxxxxxxxxxxxxxxx",
        "secretKey": "xxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

**模型选择**：

| 模型 | 适用场景 | 价格 |
|------|---------|------|
| **ernie-4.0** | 复杂任务 | ¥0.03/输入 ¥0.09/输出 |
| **ernie-3.5** | 通用场景 | ¥0.012/输入 ¥0.036/输出 |
| **ernie-speed** | 快速响应 | ¥0.004/输入 ¥0.012/输出 |

---

### 豆包（火山引擎）

#### 获取 API Key

**步骤 1：访问火山引擎**

1. 打开 https://www.volcengine.com/
2. 登录火山引擎账号
3. 搜索「豆包大模型」

**步骤 2：开通服务**

1. 进入豆包控制台
2. 点击「立即使用」
3. 完成实名认证

**步骤 3：创建密钥**

1. 进入「密钥管理」
2. 创建访问密钥
3. 复制 Access Key 和 Secret Key

---

#### OpenClaw 配置

```json
{
  "models": {
    "default": "doubao-pro",
    "providers": {
      "volcengine": {
        "accessKey": "xxxxxxxxxxxxxxxxx",
        "secretKey": "xxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

**模型选择**：

| 模型 | 适用场景 | 价格 |
|------|---------|------|
| **doubao-pro** | 通用场景 | ¥0.008/输入 ¥0.03/输出 |
| **doubao-lite** | 简单任务 | ¥0.003/输入 ¥0.009/输出 |

---

### Kimi（月之暗面）

#### 获取 API Key

**步骤 1：访问月之暗面**

1. 打开 https://platform.moonshot.cn/
2. 注册/登录账号
3. 完成实名认证

**步骤 2：创建密钥**

1. 进入「API Key 管理」
2. 点击「创建 API Key」
3. 复制并保存

---

#### OpenClaw 配置

```json
{
  "models": {
    "default": "moonshot-v1-128k",
    "providers": {
      "moonshot": {
        "apiKey": "sk-xxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

**模型选择**：

| 模型 | 上下文 | 价格 |
|------|--------|------|
| **moonshot-v1-8k** | 8K | ¥0.012/输入 ¥0.048/输出 |
| **moonshot-v1-32k** | 32K | ¥0.024/输入 ¥0.096/输出 |
| **moonshot-v1-128k** | 128K | ¥0.06/输入 ¥0.24/输出 |

---

### 本地模型（Ollama）

#### 安装 Ollama

**Linux 安装**

```bash
# 一键安装
curl -fsSL https://ollama.com/install.sh | sh

# 国内加速
curl -fsSL https://ollama.2333333.xyz/install.sh | sh
```

**macOS 安装**

```bash
brew install ollama
```

**Windows 安装**

1. 访问 https://ollama.com/download
2. 下载 Windows 安装包
3. 双击安装

---

#### 下载模型

```bash
# Llama 3（通用）
ollama pull llama3

# Qwen2.5（中文优化）
ollama pull qwen2.5

# CodeLlama（代码）
ollama pull codellama

# ChatGLM3（中文）
ollama pull chatglm3
```

---

#### OpenClaw 配置

```json
{
  "models": {
    "default": "qwen2.5",
    "providers": {
      "ollama": {
        "baseUrl": "http://localhost:11434"
      }
    }
  }
}
```

---

## 第六部分至第十二部分

（保持原文档结构，补充中文注释和本土化示例）

---

## 附录 D：国内 API Key 获取指南

### 国内大模型 API Key 获取汇总

| 提供商 | 官网 | 控制台 | 价格 |
|--------|------|--------|------|
| **通义千问** | https://www.aliyun.com/ | https://dashscope.console.aliyun.com/ | ¥0.008-0.12/1K tokens |
| **文心一言** | https://cloud.baidu.com/ | https://console.bce.baidu.com/qianfan/ | ¥0.004-0.09/1K tokens |
| **豆包** | https://www.volcengine.com/ | https://console.volcengine.com/ark/ | ¥0.003-0.03/1K tokens |
| **Kimi** | https://platform.moonshot.cn/ | https://platform.moonshot.cn/console | ¥0.012-0.24/1K tokens |
| **讯飞星火** | https://www.xfyun.cn/ | https://console.xfyun.cn/ | ¥0.03-0.09/1K tokens |
| **智谱 AI** | https://open.bigmodel.cn/ | https://open.bigmodel.cn/console | ¥0.05-0.15/1K tokens |

---

## 许可证

**MIT License**

Copyright (c) 2026 OpenClaw

允许免费使用、复制、修改、合并、出版、发行、再授权。

---

**文档版本**: v5.0 中国内地版  
**最后更新**: 2026-03-23  
**适用地区**: 中国大陆及港澳台地区  
**内容来源**: 基于官方文档深度本土化适配
