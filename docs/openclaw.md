# OpenClaw 完全指南

> **自托管 AI 网关 · 多聊天平台统一接入 · 7×24 小时自动化 AI 助手**

**版本**: v2026.03.23（基于官方文档完整提取）  
**许可证**: MIT  
**官方文档**: https://docs.openclaw.ai/  
**GitHub**: https://github.com/openclaw/openclaw  
**Discord**: https://discord.com/invite/clawd

---

## 📑 目录

- [第一部分：产品认知与快速入门](#第一部分产品认知与快速入门)
  - [1.1 什么是 OpenClaw](#11-什么是-openclaw)
  - [1.2 核心价值与定位](#12-核心价值与定位)
  - [1.3 适用场景](#13-适用场景)
  - [1.4 快速开始（60 秒上手）](#14-快速开始 60 秒上手)
  - [1.5 系统要求与兼容性](#15-系统要求与兼容性)
- [第二部分：安装与部署](#第二部分安装与部署)
  - [2.1 安装方式对比](#21-安装方式对比)
  - [2.2 npm 安装（推荐）](#22-npm-安装推荐)
  - [2.3 Docker 容器化部署](#23-docker-容器化部署)
  - [2.4 源码安装（开发者）](#24-源码安装开发者)
  - [2.5 离线安装方案](#25-离线安装方案)
  - [2.6 生产环境部署](#26-生产环境部署)
  - [2.7 升级与回滚](#27-升级与回滚)
- [第三部分：核心概念](#第三部分核心概念)
  - [3.1 架构概览](#31-架构概览)
  - [3.2 Gateway（网关）](#32-gateway 网关)
  - [3.3 Agent（智能体）](#33-agent 智能体)
  - [3.4 Channel（渠道）](#34-channel 渠道)
  - [3.5 Session（会话）](#35-session 会话)
  - [3.6 Memory（记忆）](#36-memory 记忆)
  - [3.7 Context（上下文）](#37-context 上下文)
  - [3.8 Agent Loop（智能体循环）](#38-agent-loop 智能体循环)
  - [3.9 System Prompt（系统提示词）](#39-system-prompt 系统提示词)
  - [3.10 Compaction（自动压缩）](#310-compaction 自动压缩)
- [第四部分：渠道配置](#第四部分渠道配置)
  - [4.1 支持的渠道列表](#41-支持的渠道列表)
  - [4.2 Telegram 配置详解](#42-telegram-配置详解)
  - [4.3 WhatsApp 配置详解](#43-whatsapp-配置详解)
  - [4.4 Discord 配置详解](#44-discord-配置详解)
  - [4.5 iMessage 配置（BlueBubbles）](#45-imessage-配置 bluebubbles)
  - [4.6 其他渠道配置](#46-其他渠道配置)
  - [4.7 渠道路由规则](#47-渠道路由规则)
  - [4.8 访问控制与安全](#48-访问控制与安全)
- [第五部分：模型与提供商](#第五部分模型与提供商)
  - [5.1 模型选择指南](#51-模型选择指南)
  - [5.2 支持的模型提供商](#52-支持的模型提供商)
  - [5.3 模型配置与切换](#53-模型配置与切换)
  - [5.4 模型故障转移](#54-模型故障转移)
  - [5.5 Token 使用与成本优化](#55-token-使用与成本优化)
  - [5.6 本地模型部署](#56-本地模型部署)
- [第六部分：Agent 与工具](#第六部分 agent 与工具)
  - [6.1 Agent 工作区配置](#61-agent-工作区配置)
  - [6.2 工具与插件系统](#62-工具与插件系统)
  - [6.3 MCP 协议集成](#63-mcp-协议集成)
  - [6.4 子 Agent 与任务分发](#64-子-agent 与任务分发)
  - [6.5 定时任务与自动化](#65-定时任务与自动化)
- [第七部分：会话与记忆管理](#第七部分会话与记忆管理)
  - [7.1 会话管理深度解析](#71-会话管理深度解析)
  - [7.2 记忆系统架构](#72-记忆系统架构)
  - [7.3 会话压缩机制](#73-会话压缩机制)
  - [7.4 会话清理与维护](#74-会话清理与维护)
- [第八部分：运维与安全](#第八部分运维与安全)
  - [8.1 Gateway 运维管理](#81-gateway-运维管理)
  - [8.2 日志与调试](#82-日志与调试)
  - [8.3 监控与告警](#83-监控与告警)
  - [8.4 备份与恢复](#84-备份与恢复)
  - [8.5 安全配置](#85-安全配置)
  - [8.6 性能优化](#86-性能优化)
- [第九部分：故障排查与 FAQ](#第九部分故障排查与-faq)
  - [9.1 诊断命令速查](#91-诊断命令速查)
  - [9.2 高频问题解决方案](#92-高频问题解决方案)
  - [9.3 FAQ（50+ 常见问题）](#93-faq50-常见问题)
  - [9.4 开发者支持](#94-开发者支持)
- [附录](#附录)
  - [附录 A：环境变量参考](#附录 a 环境变量参考)
  - [附录 B：配置文件完整参考](#附录 b 配置文件完整参考)
  - [附录 C：CLI 命令参考](#附录 c-cli-命令参考)
  - [附录 D：目录结构与文件位置](#附录 d 目录结构与文件位置)

---

## 第一部分：产品认知与快速入门

### 1.1 什么是 OpenClaw

**OpenClaw** 是一个**自托管 AI 网关**（Self-hosted AI Gateway），让你能够在自己的服务器上运行私人 AI 助手，并通过任意聊天平台（Telegram、WhatsApp、Discord、iMessage 等）进行交互。

#### 核心定义

| 术语 | 定义 |
|------|------|
| **自托管** | 运行在你控制的服务器上，数据完全本地化，无需依赖第三方 SaaS |
| **AI 网关** | 统一管理多个 AI 模型提供商（Anthropic、OpenAI、Google 等）的中间层 |
| **多渠道** | 支持 30+ 聊天平台，一套配置即可连接 Telegram、WhatsApp、Discord 等 |
| **7×24 小时** | 持续运行，可执行定时任务、后台监控、自动化工作流 |

#### 一句话总结

> OpenClaw = 你的私人 AI 助手 + 任意聊天平台 + 自托管控制 + 多模型支持

---

### 1.2 核心价值与定位

#### 与传统 AI 聊天工具的对比

| 维度 | 传统 AI 工具（ChatGPT/Claude） | OpenClaw |
|------|-------------------------------|----------|
| **数据隐私** | 数据存储在提供商服务器 | 数据完全本地化 |
| **部署方式** | SaaS 云端服务 | 自托管（本地/VPS） |
| **聊天平台** | 仅官方 App/Web | 30+ 平台任选 |
| **自动化** | 手动交互 | 支持定时任务、后台运行 |
| **模型选择** | 单一提供商 | 30+ 提供商自由切换 |
| **成本** | 订阅费 + Token 费 | 仅 Token 费（可使用本地模型） |
| **可扩展性** | 固定功能 | 支持自定义工具、插件、MCP |

#### 与同类开源项目的对比

| 项目 | OpenClaw | Claude Code | Continue.dev |
|------|----------|-------------|--------------|
| **定位** | 全渠道 AI 网关 | CLI 编程助手 | IDE 插件 |
| **聊天平台** | 30+ | 仅 Terminal | 仅 VS Code/JetBrains |
| **自托管** | ✅ 完全支持 | ❌ 依赖 Anthropic API | ❌ 依赖 API |
| **多渠道统一** | ✅ 一套配置 | ❌ | ❌ |
| **定时任务** | ✅ 支持 | ❌ | ❌ |
| **记忆系统** | ✅ 持久化记忆 | ⚠️ 会话级 | ⚠️ 项目级 |
| **本地模型** | ✅ Ollama/vLLM | ❌ | ✅ |

#### OpenClaw 的不可替代性

1. **隐私优先**：敏感数据（代码、文档、聊天记录）完全本地存储
2. **平台自由**：不被绑定到单一聊天平台，可随时切换
3. **模型中立**：支持 30+ 提供商，避免供应商锁定
4. **自动化能力**：7×24 小时后台运行，执行定时任务、监控、工作流
5. **完全可控**：从部署到配置到扩展，全部开源可审计

---

### 1.3 适用场景

#### 个人用户场景

| 场景 | 描述 | 核心价值 |
|------|------|----------|
| **远程编码助手** | 通过 Telegram/Discord 随时向 AI 提问，获取代码建议 | 无需打开浏览器/App，聊天即编程 |
| **多设备协同** | 手机、平板、电脑通过同一渠道访问 AI | 统一上下文，跨设备无缝切换 |
| **自动化运维** | 定时检查服务器状态、备份、告警通知 | 7×24 小时无人值守 |
| **个人知识库** | 通过记忆系统存储常用信息、代码片段、笔记 | 持久化记忆，随时检索 |
| **学习助手** | 语言学习、技术问答、概念解释 | 随时提问，上下文连续 |

#### 团队场景

| 场景 | 描述 | 核心价值 |
|------|------|----------|
| **团队轻量 AI 助手** | Slack/飞书/Discord 群组接入 AI，共享上下文 | 降低协作成本，统一知识沉淀 |
| **客服自动化** | WhatsApp/Telegram 自动回复常见问题 | 减少人工客服压力 |
| **DevOps 自动化** | 自动部署、监控、告警、日志分析 | 提升运维效率 |
| **内容创作** | 自动生成博客、社交媒体内容、营销文案 | 批量生产，多平台分发 |

#### 企业场景

| 场景 | 描述 | 核心价值 |
|------|------|----------|
| **内部 AI 助手** | 企业微信/钉钉/Slack 接入，员工随时访问 | 提升工作效率，数据安全 |
| **客户支持** | 多渠道统一接入，自动分诊、智能回复 | 降低客服成本，提升响应速度 |
| **数据分析** | 定时生成报表、数据可视化、趋势分析 | 自动化决策支持 |
| **合规审计** | 所有对话记录本地存储，可审计、可追溯 | 满足合规要求 |

---

### 1.4 快速开始（60 秒上手）

#### 前置要求

- Node.js 18+（推荐 20+）
- npm 或 bun 包管理器
- Git（可选，用于源码安装）

#### 三步安装

```bash
# 1. 全局安装 OpenClaw
npm install -g openclaw

# 2. 启动 Onboarding（首次配置向导）
openclaw onboarding

# 3. 打开 Dashboard（浏览器访问）
openclaw dashboard
# 或访问 http://localhost:3000
```

#### 验证安装

```bash
# 检查状态
openclaw status

# 预期输出：
# ✅ Gateway: running
# ✅ RPC: reachable
# ✅ Config: loaded
# ✅ Models: configured
```

#### 第一个聊天

1. 在 Dashboard 中选择渠道（如 Telegram）
2. 按照指引完成 Bot Token 配置
3. 在 Telegram 中向 Bot 发送 `/start`
4. 开始对话！

---

### 1.5 系统要求与兼容性

#### 操作系统支持

| 系统 | 最低版本 | 推荐版本 | 备注 |
|------|---------|---------|------|
| **Linux** | Ubuntu 20.04 / CentOS 8 | Ubuntu 22.04+ / Debian 12+ | 生产环境推荐 |
| **macOS** | 12.0 (Monterey) | 14.0+ (Sonoma) | iMessage 必需 macOS |
| **Windows** | 10 (21H2) | 11 (22H2) | 需 WSL 2 或 PowerShell |
| **Docker** | 20.10+ | 24.0+ | 跨平台一致体验 |

#### CPU 架构支持

| 架构 | 支持状态 | 备注 |
|------|---------|------|
| **x86_64** | ✅ 完全支持 | 主流服务器/桌面 |
| **ARM64** | ✅ 完全支持 | Raspberry Pi 4/5、Apple Silicon |
| **ARMv7** | ⚠️ 有限支持 | Raspberry Pi 3（性能受限） |

#### 硬件要求

| 场景 | CPU | 内存 | 存储 | 网络 |
|------|-----|------|------|------|
| **最小配置** | 1 核 | 512MB | 2GB | 10Mbps |
| **个人使用** | 2 核 | 2GB | 10GB | 50Mbps |
| **团队使用** | 4 核 | 4GB | 50GB | 100Mbps |
| **生产环境** | 8 核+ | 8GB+ | 100GB+ | 1Gbps+ |

#### Node.js 版本兼容性

| Node.js 版本 | 支持状态 | 备注 |
|-------------|---------|------|
| **18.x** | ✅ 支持（LTS） | 最低要求 |
| **20.x** | ✅ 推荐（LTS） | 最佳兼容性 |
| **21.x** | ✅ 支持 | 最新特性 |
| **22.x** | ⚠️ 测试中 | 可能存在兼容性问题 |
| **< 18.x** | ❌ 不支持 | 请使用 LTS 版本 |

#### 隐藏依赖

| 依赖 | 用途 | 安装命令 |
|------|------|---------|
| **Git** | 源码安装、技能管理 | `apt install git` / `brew install git` |
| **Python 3** | 部分技能执行 | `apt install python3` |
| **Docker** | 容器化部署（可选） | `apt install docker.io` |
| **systemd** | Linux 服务管理 | 默认已安装 |

#### 国内网络环境适配

```bash
# 使用国内镜像源安装
npm config set registry https://registry.npmmirror.com
npm install -g openclaw

# 或使用代理
export HTTPS_PROXY=http://127.0.0.1:7890
npm install -g openclaw
```

---

### 1.6 核心术语对照表

| 英文术语 | 中文翻译 | 定义 |
|---------|---------|------|
| **Gateway** | 网关 | OpenClaw 的核心服务，处理所有请求路由、模型调用、渠道通信 |
| **Agent** | 智能体 | 具有特定角色和能力的 AI 实例（如编程助手、客服机器人） |
| **Channel** | 渠道 | 聊天平台连接（Telegram、WhatsApp、Discord 等） |
| **Session** | 会话 | 一次连续的对话上下文，包含历史消息和记忆 |
| **Node** | 节点 | 连接到 Gateway 的远程执行单元（用于分布式部署） |
| **RPC** | 远程过程调用 | Gateway 与 CLI/Dashboard 之间的通信协议 |
| **Pi Agent** | 轻量智能体 | 运行在资源受限设备（如 Raspberry Pi）上的简化 Agent |
| **Compaction** | 压缩 | 自动压缩长会话历史，减少 Token 消耗 |
| **Memory** | 记忆 | 持久化存储的知识库，跨会话共享 |
| **Context** | 上下文 | 当前会话中的消息历史和相关信息 |
| **System Prompt** | 系统提示词 | 定义 Agent 行为和角色的底层指令 |
| **Skill** | 技能 | Agent 可调用的工具函数（如文件操作、API 调用） |
| **MCP** | 模型上下文协议 | Model Context Protocol，标准化的工具/资源接口 |
| **Workspace** | 工作区 | 包含 Agent 配置、技能、记忆的独立环境 |
| **Auth Profile** | 认证配置 | 存储模型提供商的 API Key/OAuth Token |

---

## 第二部分：安装与部署

### 2.1 安装方式对比

| 安装方式 | 适用场景 | 优点 | 缺点 | 推荐度 |
|---------|---------|------|------|--------|
| **npm 全局安装** | 个人用户、快速上手 | 简单快捷、自动更新 | 依赖 Node.js 环境 | ⭐⭐⭐⭐⭐ |
| **Docker 容器化** | 生产环境、跨平台一致 | 隔离性好、易于部署 | 需要 Docker 知识 | ⭐⭐⭐⭐ |
| **源码安装** | 开发者、自定义需求 | 完全控制、可调试 | 需要编译、维护成本高 | ⭐⭐⭐ |
| **离线安装** | 内网环境、无网络 | 无需联网、可审计 | 手动下载、更新麻烦 | ⭐⭐ |

---

### 2.2 npm 安装（推荐）

#### 前置要求

```bash
# 检查 Node.js 版本（需要 18+）
node --version

# 检查 npm 版本
npm --version

# 升级 Node.js（如需要）
# Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# macOS
brew install node@20

# Windows（使用 nvm-windows）
# 下载：https://github.com/coreybutler/nvm-windows/releases
```

#### 安装步骤

```bash
# 1. 全局安装 OpenClaw
npm install -g openclaw

# 2. 验证安装
openclaw --version

# 3. 启动 Onboarding（首次配置向导）
openclaw onboarding

# 4. 启动 Gateway
openclaw gateway

# 5. 打开 Dashboard（新标签页）
openclaw dashboard
```

#### 国内镜像加速

```bash
# 临时使用镜像源
npm install -g openclaw --registry=https://registry.npmmirror.com

# 永久设置镜像源
npm config set registry https://registry.npmmirror.com

# 验证配置
npm config get registry
```

#### 安装问题排查

```bash
# 问题 1：权限错误（EACCES）
# 解决方案：使用 npm prefix 或 nvm
npm config set prefix ~/.npm-global
export PATH=~/.npm-global/bin:$PATH

# 问题 2：网络超时
# 解决方案：增加超时时间或使用代理
npm config set fetch-timeout 300000
npm install -g openclaw

# 问题 3：依赖安装失败
# 解决方案：清理缓存后重试
npm cache clean --force
npm install -g openclaw
```

---

### 2.3 Docker 容器化部署

#### 快速启动

```bash
# 一键启动（使用官方镜像）
docker run -d \
  --name openclaw \
  -p 3000:3000 \
  -p 8080:8080 \
  -v openclaw-data:/root/.openclaw \
  -e OPENCLAW_CONFIG_PATH=/root/.openclaw/config.json \
  openclaw/openclaw:latest

# 查看日志
docker logs -f openclaw

# 访问 Dashboard
# http://localhost:3000
```

#### Docker Compose 部署

```yaml
# docker-compose.yml
version: '3.8'

services:
  openclaw:
    image: openclaw/openclaw:latest
    container_name: openclaw
    restart: unless-stopped
    ports:
      - "3000:3000"  # Dashboard
      - "8080:8080"  # Gateway
    volumes:
      - ./config:/root/.openclaw/config
      - ./data:/root/.openclaw/data
      - ./logs:/root/.openclaw/logs
    environment:
      - OPENCLAW_CONFIG_PATH=/root/.openclaw/config/config.json
      - NODE_ENV=production
    networks:
      - openclaw-net

networks:
  openclaw-net:
    driver: bridge
```

```bash
# 启动服务
docker-compose up -d

# 查看状态
docker-compose ps

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down
```

#### 自定义 Docker 镜像

```dockerfile
# Dockerfile
FROM openclaw/openclaw:latest

# 安装额外依赖
RUN apt update && apt install -y \
    python3 \
    python3-pip \
    git \
    && rm -rf /var/lib/apt/lists/*

# 复制自定义配置
COPY config.json /root/.openclaw/config/
COPY skills/ /root/.openclaw/skills/

# 设置环境变量
ENV OPENCLAW_CONFIG_PATH=/root/.openclaw/config/config.json

EXPOSE 3000 8080

CMD ["openclaw", "gateway"]
```

```bash
# 构建镜像
docker build -t my-openclaw:latest .

# 运行容器
docker run -d \
  --name my-openclaw \
  -p 3000:3000 \
  -p 8080:8080 \
  my-openclaw:latest
```

---

### 2.4 源码安装（开发者）

#### 克隆仓库

```bash
# 克隆源码
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 查看可用版本
git tag -l

# 切换到稳定版本
git checkout v0.1.0
```

#### 安装依赖

```bash
# 安装 Node.js 依赖
npm install

# 或使用 bun（更快）
bun install
```

#### 构建与运行

```bash
# 开发模式运行
npm run dev

# 生产模式构建
npm run build

# 运行 Gateway
npm run gateway

# 运行 Dashboard
npm run dashboard
```

#### 本地开发调试

```bash
# 启用调试模式
export DEBUG=openclaw:*
npm run dev

# 查看调试日志
# 输出包含详细的请求/响应、数据库操作、渠道通信等
```

---

### 2.5 离线安装方案

#### 准备离线包

```bash
# 在有网络的机器上下载
npm pack openclaw

# 下载依赖包
npm install openclaw --package-lock-only
npm ci --package-lock-only

# 打包所有文件
tar -czvf openclaw-offline.tar.gz \
    openclaw-*.tgz \
    node_modules/ \
    package.json \
    package-lock.json
```

#### 离线安装

```bash
# 传输到目标机器
scp openclaw-offline.tar.gz user@target:/tmp/

# 解压并安装
cd /tmp
tar -xzvf openclaw-offline.tar.gz
npm install -g openclaw-*.tgz

# 验证安装
openclaw --version
```

---

### 2.6 生产环境部署

#### systemd 服务配置

```ini
# /etc/systemd/system/openclaw.service
[Unit]
Description=OpenClaw AI Gateway
After=network.target

[Service]
Type=simple
User=openclaw
Group=openclaw
WorkingDirectory=/opt/openclaw
Environment=NODE_ENV=production
Environment=OPENCLAW_CONFIG_PATH=/etc/openclaw/config.json
ExecStart=/usr/bin/openclaw gateway
Restart=always
RestartSec=10
StandardOutput=journal
StandardError=journal
SyslogIdentifier=openclaw

# 安全加固
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=/var/lib/openclaw

[Install]
WantedBy=multi-user.target
```

```bash
# 创建用户
sudo useradd -r -s /bin/false openclaw

# 安装 OpenClaw
sudo npm install -g openclaw --prefix /opt/openclaw

# 创建配置目录
sudo mkdir -p /etc/openclaw
sudo mkdir -p /var/lib/openclaw

# 设置权限
sudo chown -R openclaw:openclaw /opt/openclaw
sudo chown -R openclaw:openclaw /var/lib/openclaw

# 启用服务
sudo systemctl daemon-reload
sudo systemctl enable openclaw
sudo systemctl start openclaw

# 查看状态
sudo systemctl status openclaw

# 查看日志
sudo journalctl -u openclaw -f
```

#### Nginx 反向代理

```nginx
# /etc/nginx/sites-available/openclaw
server {
    listen 80;
    server_name openclaw.example.com;

    # 重定向到 HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name openclaw.example.com;

    # SSL 证书
    ssl_certificate /etc/letsencrypt/live/openclaw.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/openclaw.example.com/privkey.pem;

    # 安全头
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;

    # Dashboard
    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Gateway WebSocket
    location /ws {
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_read_timeout 86400;
    }
}
```

```bash
# 测试配置
sudo nginx -t

# 重新加载
sudo systemctl reload nginx

# 申请 SSL 证书
sudo certbot --nginx -d openclaw.example.com
```

---

### 2.7 升级与回滚

#### 升级流程

```bash
# 检查可用版本
npm view openclaw versions

# 升级到最新版
npm install -g openclaw@latest

# 升级到指定版本
npm install -g openclaw@0.1.0

# 验证升级
openclaw --version

# 重启服务
sudo systemctl restart openclaw
```

#### 回滚流程

```bash
# 回滚到上一版本
npm install -g openclaw@$(npm view openclaw versions --json | jq -r '.[-2]')

# 回滚到指定版本
npm install -g openclaw@0.0.9

# 恢复配置文件（如有需要）
cp /etc/openclaw/config.json.bak /etc/openclaw/config.json

# 重启服务
sudo systemctl restart openclaw
```

#### 升级前备份

```bash
# 备份配置
cp -r /etc/openclaw /etc/openclaw.bak.$(date +%Y%m%d)

# 备份数据
cp -r /var/lib/openclaw /var/lib/openclaw.bak.$(date +%Y%m%d)

# 备份日志（可选）
tar -czvf /backup/openclaw-logs-$(date +%Y%m%d).tar.gz /var/log/openclaw/
```

---

## 第三部分：核心概念

### 3.1 架构概览

```
┌─────────────────────────────────────────────────────────────┐
│                      用户设备                                │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐       │
│  │Telegram │  │WhatsApp │  │ Discord │  │ 其他渠道 │       │
│  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘       │
│       │            │            │            │              │
└───────┼────────────┼────────────┼────────────┼──────────────┘
        │            │            │            │
        └────────────┴──────┬─────┴────────────┘
                            │
                    ┌───────▼────────┐
                    │    Gateway     │
                    │   (端口 8080)   │
                    └───────┬────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
┌───────▼───────┐   ┌──────▼──────┐   ┌───────▼───────┐
│    Dashboard  │   │    Agent    │   │  Model Provider│
│   (端口 3000) │   │  (工作区)   │   │ (API/本地)    │
└───────────────┘   └──────┬──────┘   └───────────────┘
                           │
                    ┌──────▼──────┐
                    │   Memory    │
                    │  (持久化)   │
                    └─────────────┘
```

#### 组件说明

| 组件 | 端口 | 职责 |
|------|------|------|
| **Gateway** | 8080 | 核心服务，处理所有渠道通信、模型调用、路由 |
| **Dashboard** | 3000 | Web 管理界面，配置管理、监控、日志查看 |
| **Agent** | - | 智能体实例，包含配置、技能、记忆 |
| **Memory** | - | 持久化存储，跨会话共享知识 |

---

### 3.2 Gateway（网关）

#### 核心职责

1. **请求路由**：接收来自渠道的消息，路由到对应 Agent
2. **模型调用**：调用配置的模型提供商 API
3. **会话管理**：维护 Session 状态和上下文
4. **记忆系统**：读写 Memory，支持语义搜索
5. **工具执行**：执行 Agent 调用的技能和工具

#### Gateway 状态检查

```bash
# 快速状态检查
openclaw gateway status

# 输出示例：
# Runtime: running
# RPC probe: reachable
# Config: loaded from /etc/openclaw/config.json
# Port: 8080 (listening)

# 深度健康检查
openclaw health --verbose

# JSON 格式输出
openclaw health --json
```

#### Gateway 配置

```json
{
  "gateway": {
    "port": 8080,
    "bind": "0.0.0.0",
    "cors": {
      "enabled": true,
      "origins": ["http://localhost:3000"]
    },
    "auth": {
      "token": "your-secret-token",
      "allowFrom": ["127.0.0.1", "192.168.1.0/24"]
    }
  }
}
```

---

### 3.3 Agent（智能体）

#### Agent 类型

| 类型 | 描述 | 适用场景 |
|------|------|----------|
| **通用 Agent** | 默认配置，全能型助手 | 日常对话、问答 |
| **编程 Agent** | 专注代码生成、调试 | 开发辅助 |
| **客服 Agent** | 预设回复模板、礼貌用语 | 客户服务 |
| **分析 Agent** | 数据处理、图表生成 | 数据分析 |
| **Pi Agent** | 轻量级，资源占用少 | Raspberry Pi 等 |

#### Agent 配置文件

```json
{
  "agents": {
    "default": {
      "model": "anthropic/claude-sonnet-4-20250514",
      "systemPrompt": "你是一个有帮助的 AI 助手。",
      "skills": ["file_ops", "web_search", "code_execution"],
      "memory": {
        "enabled": true,
        "maxSize": 1000
      },
      "context": {
        "maxTokens": 8192,
        "compaction": {
          "enabled": true,
          "threshold": 0.8
        }
      }
    }
  }
}
```

---

### 3.4 Channel（渠道）

#### 渠道分类

| 类别 | 渠道 | 特点 |
|------|------|------|
| **即时通讯** | Telegram, WhatsApp, Signal | 个人用户首选 |
| **社区平台** | Discord, Slack, Matrix | 团队协作用 |
| **企业通讯** | 飞书，企业微信，钉钉 | 企业内部 |
| **苹果生态** | iMessage (BlueBubbles) | macOS 专属 |
| **其他** | Email, SMS, Voice | 特殊场景 |

#### 渠道配置示例

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "botToken": "BOT_TOKEN_HERE",
      "allowFrom": ["*"],
      "commands": {
        "/start": "启动对话",
        "/new": "新建会话",
        "/help": "显示帮助"
      }
    },
    "discord": {
      "enabled": true,
      "botToken": "BOT_TOKEN_HERE",
      "guilds": ["GUILD_ID"],
      "channels": ["CHANNEL_ID"]
    }
  }
}
```

---

### 3.5 Session（会话）

#### 会话生命周期

```
创建 → 活动 → 压缩 → 归档 → 清理
  │      │      │      │      │
  │      │      │      │      └─ 超过保留期
  │      │      │      └─ 长期未使用
  │      │      └─ 上下文接近限制
  │      └─ 用户交互
  └─ 首次消息
```

#### 会话管理命令

```bash
# 列出所有会话
openclaw session list

# 查看会话详情
openclaw session get SESSION_ID

# 删除会话
openclaw session delete SESSION_ID

# 清空所有会话
openclaw session purge

# 导出会话
openclaw session export SESSION_ID --format json
```

---

### 3.6 Memory（记忆）

#### 记忆系统架构

```
┌─────────────────────────────────────┐
│          Memory Manager             │
├─────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  │
│  │ Short-term  │  │  Long-term  │  │
│  │  (Context)  │  │  (Storage)  │  │
│  └─────────────┘  └─────────────┘  │
│  ┌─────────────┐  ┌─────────────┐  │
│  │   Semantic  │  │   Keyword   │  │
│  │   Search    │  │   Search    │  │
│  └─────────────┘  └─────────────┘  │
└─────────────────────────────────────┘
```

#### 记忆文件结构

```
~/.openclaw/memory/
├── short_term/      # 短期记忆（会话级）
├── long_term/       # 长期记忆（持久化）
├── semantic/        # 语义索引
└── config.json      # 记忆配置
```

---

### 3.7 Context（上下文）

#### 上下文组成

| 组成部分 | 描述 | Token 占比 |
|---------|------|-----------|
| **系统提示词** | Agent 角色定义 | ~500 |
| **历史消息** | 最近 N 轮对话 | ~4000-8000 |
| **记忆检索** | 相关记忆片段 | ~1000-2000 |
| **工具结果** | 技能执行输出 | ~500-2000 |
| **用户消息** | 当前输入 | ~100-500 |

#### 上下文管理策略

```json
{
  "context": {
    "maxTokens": 8192,
    "strategy": "sliding_window",
    "reserveTokens": 1000,
    "compaction": {
      "enabled": true,
      "threshold": 0.8,
      "method": "summarize"
    }
  }
}
```

---

### 3.8 Agent Loop（智能体循环）

#### 循环流程

```
1. 接收消息
       ↓
2. 解析意图
       ↓
3. 检索记忆
       ↓
4. 选择工具
       ↓
5. 执行工具
       ↓
6. 生成回复
       ↓
7. 发送响应
       ↓
8. 更新记忆
       ↓
（回到步骤 1，等待下一条消息）
```

#### 循环配置

```json
{
  "agentLoop": {
    "maxIterations": 10,
    "timeout": 300,
    "retryOnFailure": true,
    "maxRetries": 3,
    "tools": {
      "enabled": true,
      "requireApproval": ["shell_exec", "file_write"]
    }
  }
}
```

---

### 3.9 System Prompt（系统提示词）

#### 提示词结构

```
你是一名 {角色}，专注于 {领域}。

## 能力
- 能力 1
- 能力 2
- 能力 3

## 约束
- 不做 X
- 不回答 Y
- 优先使用 Z 方法

## 风格
- 语气：{正式/随意/专业}
- 语言：{中文/英文}
- 格式：{简洁/详细}
```

#### 示例提示词

```markdown
你是一名资深软件工程师，专注于 Python 和 Web 开发。

## 能力
- 代码编写、审查、调试
- 架构设计、最佳实践
- 性能优化、安全加固

## 约束
- 不提供可执行恶意代码
- 不绕过安全机制
- 优先使用标准库和成熟框架

## 风格
- 语气：专业但友好
- 语言：中文（技术术语保留英文）
- 格式：代码示例 + 文字解释
```

---

### 3.10 Compaction（自动压缩）

#### 压缩触发条件

| 条件 | 阈值 | 动作 |
|------|------|------|
| **Token 使用率** | > 80% | 触发压缩 |
| **消息数量** | > 100 条 | 触发压缩 |
| **会话时长** | > 24 小时 | 触发压缩 |
| **手动触发** | 用户命令 | 立即压缩 |

#### 压缩方法

| 方法 | 描述 | 适用场景 |
|------|------|----------|
| **Summarize** | AI 生成摘要 | 通用场景 |
| **Truncate** | 截断旧消息 | 快速压缩 |
| **Archive** | 归档到存储 | 长期保留 |
| **Hybrid** | 摘要 + 关键消息 | 平衡质量与速度 |

#### 压缩配置

```json
{
  "compaction": {
    "enabled": true,
    "threshold": 0.8,
    "method": "hybrid",
    "preserveSystemPrompt": true,
    "preserveLastN": 10,
    "summaryModel": "anthropic/claude-haiku-3"
  }
}
```

---

## 第四部分：渠道配置

### 4.1 支持的渠道列表

#### 完整渠道列表（30+）

| 渠道 | 类型 | 配置难度 | 备注 |
|------|------|---------|------|
| **Telegram** | IM | ⭐ | 最易用，推荐首选 |
| **WhatsApp** | IM | ⭐⭐ | 需要 Meta 开发者账号 |
| **Discord** | 社区 | ⭐ | 开发者友好 |
| **Slack** | 企业 | ⭐⭐ | 需要 Workspace |
| **Signal** | IM | ⭐⭐⭐ | 需要注册手机号 |
| **Matrix** | 去中心化 | ⭐⭐ | 自建服务器 |
| **iMessage** | IM | ⭐⭐⭐⭐ | 仅 macOS，需 BlueBubbles |
| **微信** | IM | ⭐⭐⭐⭐ | 需要第三方桥接 |
| **飞书** | 企业 | ⭐⭐ | 企业账号 |
| **钉钉** | 企业 | ⭐⭐ | 企业账号 |
| **企业微信** | 企业 | ⭐⭐ | 企业账号 |
| **LINE** | IM | ⭐⭐ | 亚洲流行 |
| **KakaoTalk** | IM | ⭐⭐ | 韩国流行 |
| **Viber** | IM | ⭐⭐ | 东欧流行 |
| **Email** | 邮件 | ⭐ | SMTP/IMAP |
| **SMS** | 短信 | ⭐⭐⭐ | 需要网关服务 |
| **Voice** | 语音 | ⭐⭐⭐⭐ | Twilio 等 |
| **Mattermost** | 社区 | ⭐ | 自托管 Slack 替代 |
| **Rocket.Chat** | 社区 | ⭐ | 自托管 |
| **IRC** | 老牌 | ⭐ | 传统协议 |
| **Nextcloud Talk** | 企业 | ⭐⭐ | Nextcloud 生态 |
| **Synology Chat** | 企业 | ⭐ | 群晖 NAS |
| **Zalo** | IM | ⭐⭐ | 越南流行 |
| **Nostr** | 去中心化 | ⭐⭐⭐ | 新兴协议 |
| **Tlon** | 去中心化 | ⭐⭐⭐ | Urbit 生态 |
| **Twitch** | 直播 | ⭐⭐ | 聊天室 |
| **YouTube** | 视频 | ⭐⭐ | 直播聊天 |
| **Twitter/X** | 社交 | ⭐⭐⭐ | API 限制 |
| **Facebook** | 社交 | ⭐⭐⭐ | API 限制 |
| **Instagram** | 社交 | ⭐⭐⭐ | API 限制 |

---

### 4.2 Telegram 配置详解

#### 创建 Bot

1. 打开 Telegram，搜索 `@BotFather`
2. 发送 `/newbot` 命令
3. 按提示设置 Bot 名称和用户名
4. 获取 Bot Token（格式：`123456789:ABCdefGHIjklMNOpqrsTUVwxyz`）

#### 配置 OpenClaw

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "botToken": "123456789:ABCdefGHIjklMNOpqrsTUVwxyz",
      "allowFrom": ["*"],
      "commands": {
        "/start": "👋 欢迎使用 OpenClaw！发送 /help 查看帮助。",
        "/new": "🆕 已创建新会话",
        "/help": "📖 帮助文档：https://docs.openclaw.ai",
        "/status": "📊 当前状态：在线",
        "/reset": "🔄 已重置对话上下文"
      },
      "webhook": {
        "enabled": false,
        "url": "https://your-domain.com/telegram/webhook"
      }
    }
  }
}
```

#### 获取用户 ID

```bash
# 向 Bot 发送任意消息
# 然后查看日志获取用户 ID
openclaw logs --follow | grep telegram

# 或使用 getUpdates API
curl "https://api.telegram.org/bot<BOT_TOKEN>/getUpdates"
```

#### 限制访问用户

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "botToken": "YOUR_TOKEN",
      "allowFrom": ["123456789", "987654321"],
      "blockFrom": ["111222333"]
    }
  }
}
```

---

### 4.3 WhatsApp 配置详解

#### 前置要求

- Meta 开发者账号
- WhatsApp Business API 访问权限
- 已验证的 Facebook 商务账号

#### 创建 WhatsApp Business App

1. 访问 https://developers.facebook.com/
2. 创建新应用 → 选择"Business"
3. 添加 WhatsApp 产品
4. 获取 Phone Number ID 和 Access Token

#### 配置 OpenClaw

```json
{
  "channels": {
    "whatsapp": {
      "enabled": true,
      "phoneNumberId": "123456789012345",
      "accessToken": "EAABsbCS1iHgBO...",
      "verifyToken": "your_verify_token",
      "allowFrom": ["*"],
      "webhook": {
        "url": "https://your-domain.com/whatsapp/webhook",
        "verifyToken": "your_verify_token"
      }
    }
  }
}
```

#### 获取 JID（群聊 ID）

```bash
# 向 Bot 发送消息后查看日志
openclaw logs --follow | grep whatsapp

# JID 格式：1234567890@c.us (个人) 或 1234567890-1234567890@g.us (群组)
```

---

### 4.4 Discord 配置详解

#### 创建 Discord Bot

1. 访问 https://discord.com/developers/applications
2. 创建新应用
3. 进入"Bot"标签页，点击"Add Bot"
4. 复制 Bot Token
5. 启用以下 Privileged Gateway Intents：
   - MESSAGE CONTENT INTENT
   - SERVER MEMBERS INTENT

#### 邀请 Bot 到服务器

```
https://discord.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&permissions=274878024768&scope=bot
```

#### 配置 OpenClaw

```json
{
  "channels": {
    "discord": {
      "enabled": true,
      "botToken": "YOUR_BOT_TOKEN",
      "guilds": ["GUILD_ID_1", "GUILD_ID_2"],
      "channels": ["CHANNEL_ID_1"],
      "allowFrom": ["*"],
      "prefix": "!"
    }
  }
}
```

#### 获取服务器/频道 ID

1. 在 Discord 设置中启用"开发者模式"
2. 右键点击服务器/频道 → "复制 ID"

---

### 4.5 iMessage 配置（BlueBubbles）

#### 前置要求

- macOS 设备（运行 BlueBubbles 服务器）
- 已登录的 Apple ID
- BlueBubbles Server 安装

#### 安装 BlueBubbles Server

```bash
# 下载 BlueBubbles Server
# https://github.com/BlueBubbles-Artificial-Intelligence/BlueBubbles-Server

# 安装（macOS）
brew install --cask bluebubbles-server

# 启动并配置
open /Applications/BlueBubbles\ Server.app
```

#### 配置 OpenClaw

```json
{
  "channels": {
    "imessage": {
      "enabled": true,
      "bluebubblesUrl": "https://your-bluebubbles-server.com",
      "bluebubblesToken": "YOUR_BB_TOKEN",
      "allowFrom": ["+861234567890"],
      "handleType": "phone"
    }
  }
}
```

---

### 4.6 其他渠道配置

#### Slack 配置

```json
{
  "channels": {
    "slack": {
      "enabled": true,
      "botToken": "xoxb-YOUR-TOKEN",
      "signingSecret": "YOUR_SIGNING_SECRET",
      "channels": ["C01234567890"],
      "allowFrom": ["*"]
    }
  }
}
```

#### Email 配置

```json
{
  "channels": {
    "email": {
      "enabled": true,
      "smtp": {
        "host": "smtp.gmail.com",
        "port": 587,
        "secure": false,
        "auth": {
          "user": "your-email@gmail.com",
          "pass": "your-app-password"
        }
      },
      "imap": {
        "host": "imap.gmail.com",
        "port": 993,
        "secure": true,
        "auth": {
          "user": "your-email@gmail.com",
          "pass": "your-app-password"
        }
      },
      "allowFrom": ["trusted@example.com"]
    }
  }
}
```

---

### 4.7 渠道路由规则

#### 基础路由

```json
{
  "routing": {
    "rules": [
      {
        "name": "telegram-to-default",
        "from": { "channel": "telegram" },
        "to": { "agent": "default" }
      },
      {
        "name": "discord-coding",
        "from": { "channel": "discord", "channelId": "123456" },
        "to": { "agent": "coding-assistant" }
      }
    ]
  }
}
```

#### 条件路由

```json
{
  "routing": {
    "rules": [
      {
        "name": "urgent-to-human",
        "from": { "channel": "*" },
        "condition": { "contains": ["urgent", "emergency"] },
        "to": { "action": "escalate", "target": "human-agent" }
      },
      {
        "name": "code-to-coding-agent",
        "from": { "channel": "*" },
        "condition": { "containsCode": true },
        "to": { "agent": "coding-assistant" }
      }
    ]
  }
}
```

---

### 4.8 访问控制与安全

#### IP 白名单

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "allowFrom": ["192.168.1.0/24", "10.0.0.0/8"],
      "blockFrom": ["203.0.113.0/24"]
    }
  }
}
```

#### 用户白名单

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "allowedUsers": ["123456789", "987654321"],
      "blockedUsers": ["111222333"]
    }
  }
}
```

#### 速率限制

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "rateLimit": {
        "messagesPerMinute": 10,
        "messagesPerHour": 100,
        "blockDuration": 300
      }
    }
  }
}
```

---

## 第五部分：模型与提供商

### 5.1 模型选择指南

#### 按场景选择模型

| 场景 | 推荐模型 | 理由 | 成本估算 |
|------|---------|------|---------|
| **日常对话** | Claude Haiku / GPT-4o-mini | 快速、便宜 | $0.25/1M tokens |
| **代码生成** | Claude Sonnet / GPT-4o | 代码能力强 | $3-15/1M tokens |
| **复杂推理** | Claude Opus / GPT-4 | 推理能力最强 | $15-75/1M tokens |
| **长文档处理** | Claude 200K / Gemini 2M | 上下文窗口大 | $3-15/1M tokens |
| **实时响应** | Haiku / Fast models | 延迟低 | $0.25/1M tokens |
| **多语言** | GPT-4o / Gemini | 多语言支持好 | $3-15/1M tokens |

---

### 5.2 支持的模型提供商

#### 主流提供商

| 提供商 | 模型示例 | API 类型 | 备注 |
|--------|---------|---------|------|
| **Anthropic** | claude-sonnet-4, claude-opus-4 | API Key | 代码能力强 |
| **OpenAI** | gpt-4o, gpt-4-turbo, gpt-3.5-turbo | API Key | 生态最完善 |
| **Google** | gemini-2.0-pro, gemini-2.0-flash | API Key / OAuth | 免费额度高 |
| **xAI** | grok-2, grok-2-vision | API Key | Elon Musk 旗下 |

#### 中国提供商

| 提供商 | 模型示例 | API 类型 | 备注 |
|--------|---------|---------|------|
| **阿里云** | qwen-max, qwen-plus | API Key | 中文能力强 |
| **百度** | ernie-bot-4.0 | API Key | 国内部署 |
| **智谱 AI** | glm-4, glm-4v | API Key | 开源模型 |
| **月之暗面** | moonshot-v1-8k/32k/128k | API Key | 长上下文 |
| **MiniMax** | minimax-01 | API Key | 多模态 |
| **火山引擎** | doubao-pro-4k/32k | API Key | 字节旗下 |
| **Z.AI** | z-ai-gl | API Key | 新晋厂商 |

#### 平台提供商

| 平台 | 特点 | 支持模型 |
|------|------|---------|
| **OpenRouter** | 聚合多个提供商 | 50+ 模型 |
| **Amazon Bedrock** | AWS 生态 | Claude, Llama, Titan |
| **Cloudflare AI** | 边缘计算 | 多种开源模型 |
| **Vercel AI** | 前端友好 | 主流模型 |
| **Together AI** | 开源模型托管 | Llama, Mistral 等 |
| **Groq** | 超快推理 | Llama, Mixtral |
| **Anyscale** | 企业级部署 | 开源模型 |
| **Perplexity** | 搜索增强 | 自研 + 第三方 |
| **DeepInfra** | 低价开源模型 | 多种 Llama 变体 |
| **Fireworks AI** | 多模态 | Llama, FLUX |

#### 本地部署

| 方案 | 特点 | 适用场景 |
|------|------|----------|
| **Ollama** | 一键部署 | 个人开发 |
| **vLLM** | 高性能推理 | 生产环境 |
| **SGLang** | 结构化生成 | 特定任务 |
| **llama.cpp** | CPU 友好 | 资源受限 |
| **TGI** | HuggingFace 官方 | 企业部署 |

---

### 5.3 模型配置与切换

#### 配置默认模型

```json
{
  "models": {
    "default": "anthropic/claude-sonnet-4-20250514",
    "fallback": ["openai/gpt-4o", "google/gemini-2.0-pro"],
    "aliases": {
      "fast": "anthropic/claude-haiku-3",
      "smart": "anthropic/claude-opus-4",
      "coder": "openai/gpt-4o"
    }
  }
}
```

#### 运行时切换模型

```bash
# 临时切换（当前会话）
openclaw model use anthropic/claude-opus-4

# 设置默认模型
openclaw model default anthropic/claude-sonnet-4

# 查看当前模型
openclaw model current

# 列出可用模型
openclaw model list
```

#### 按 Agent 配置模型

```json
{
  "agents": {
    "coding": {
      "model": "anthropic/claude-sonnet-4",
      "fallback": ["openai/gpt-4o"]
    },
    "chat": {
      "model": "anthropic/claude-haiku-3",
      "fallback": ["openai/gpt-4o-mini"]
    },
    "analysis": {
      "model": "anthropic/claude-opus-4",
      "fallback": ["google/gemini-2.0-pro"]
    }
  }
}
```

---

### 5.4 模型故障转移

#### 故障转移配置

```json
{
  "models": {
    "default": "anthropic/claude-sonnet-4",
    "failover": {
      "enabled": true,
      "maxRetries": 3,
      "retryDelay": 1000,
      "fallbackChain": [
        "anthropic/claude-sonnet-4",
        "openai/gpt-4o",
        "google/gemini-2.0-pro",
        "alibaba/qwen-max"
      ]
    }
  }
}
```

#### 故障转移策略

| 策略 | 描述 | 适用场景 |
|------|------|----------|
| **顺序故障转移** | 按列表顺序尝试 | 有明确优先级 |
| **轮询故障转移** | 轮流尝试不同提供商 | 负载均衡 |
| **延迟感知** | 优先选择低延迟 | 实时应用 |
| **成本感知** | 优先选择低成本 | 预算敏感 |
| **健康检查** | 定期检查提供商状态 | 高可用要求 |

---

### 5.5 Token 使用与成本优化

#### Token 监控

```bash
# 查看 Token 使用统计
openclaw usage tokens

# 按模型统计
openclaw usage tokens --by-model

# 按渠道统计
openclaw usage tokens --by-channel

# 导出使用报告
openclaw usage export --format csv
```

#### 成本优化策略

| 策略 | 描述 | 节省比例 |
|------|------|---------|
| **使用 Haiku 等轻量模型** | 日常对话用便宜模型 | 50-90% |
| **启用上下文压缩** | 减少历史消息 Token | 20-40% |
| **缓存常用回复** | 避免重复生成 | 10-30% |
| **批量处理请求** | 合并多个小请求 | 10-20% |
| **使用本地模型** | 免费但需要硬件 | 100% |

#### 成本估算示例

```
假设每日使用量：
- 输入：100K tokens
- 输出：50K tokens

使用 Claude Sonnet-4:
- 输入：100K × $3/1M = $0.30
- 输出：50K × $15/1M = $0.75
- 日成本：$1.05
- 月成本：$31.50

使用 Claude Haiku-3（日常对话）:
- 输入：100K × $0.25/1M = $0.025
- 输出：50K × $1.25/1M = $0.0625
- 日成本：$0.0875
- 月成本：$2.63

混合使用（80% Haiku + 20% Sonnet）:
- 月成本：$8.40（节省 73%）
```

---

### 5.6 本地模型部署

#### Ollama 安装

```bash
# 安装 Ollama
curl -fsSL https://ollama.ai/install.sh | sh

# 拉取模型
ollama pull llama3.2:3b
ollama pull qwen2.5:7b
ollama pull codellama:7b

# 运行模型
ollama run llama3.2:3b
```

#### 配置 OpenClaw 使用 Ollama

```json
{
  "models": {
    "providers": {
      "ollama": {
        "baseUrl": "http://localhost:11434",
        "models": ["llama3.2:3b", "qwen2.5:7b", "codellama:7b"]
      }
    },
    "default": "ollama/llama3.2:3b"
  }
}
```

#### vLLM 部署

```bash
# 安装 vLLM
pip install vllm

# 启动服务
python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-3.2-3B-Instruct \
    --port 8000
```

```json
{
  "models": {
    "providers": {
      "vllm": {
        "baseUrl": "http://localhost:8000/v1",
        "apiKey": "EMPTY",
        "models": ["meta-llama/Llama-3.2-3B-Instruct"]
      }
    }
  }
}
```

---

## 第六部分：Agent 与工具

### 6.1 Agent 工作区配置

#### 工作区结构

```
~/.openclaw/workspaces/
├── default/
│   ├── AGENTS.md        # Agent 配置
│   ├── SOUL.md          # 核心身份定义
│   ├── MEMORY.md        # 长期记忆
│   ├── skills/          # 技能目录
│   └── memory/          # 记忆存储
├── coding/
│   ├── AGENTS.md
│   └── ...
└── research/
    ├── AGENTS.md
    └── ...
```

#### AGENTS.md 示例

```markdown
# Agent Configuration

## Identity
- Name: Coding Assistant
- Role: Senior Software Engineer
- Expertise: Python, JavaScript, System Design

## Capabilities
- Code generation and review
- Debugging and troubleshooting
- Architecture design
- Performance optimization

## Constraints
- No malicious code
- No security bypass
- Prefer standard libraries

## Tools
- file_ops: Read/write files
- shell_exec: Run commands (with approval)
- web_search: Search documentation
- code_execution: Run Python code (sandboxed)
```

---

### 6.2 工具与插件系统

#### 内置工具

| 工具 | 描述 | 权限级别 |
|------|------|---------|
| **file_ops** | 文件读写操作 | 中 |
| **shell_exec** | 执行 Shell 命令 | 高 |
| **web_search** | 网络搜索 | 低 |
| **web_fetch** | 抓取网页内容 | 低 |
| **code_execution** | 执行代码（沙箱） | 高 |
| **image_gen** | 生成图像 | 中 |
| **calculator** | 数学计算 | 低 |
| **calendar** | 日历管理 | 中 |

#### 工具配置

```json
{
  "tools": {
    "file_ops": {
      "enabled": true,
      "allowedPaths": ["/home/user/projects", "/tmp"],
      "blockedPaths": ["/etc", "/root"],
      "requireApproval": ["write", "delete"]
    },
    "shell_exec": {
      "enabled": true,
      "allowedCommands": ["ls", "cat", "grep", "git"],
      "blockedCommands": ["rm -rf", "sudo", "chmod"],
      "requireApproval": true
    }
  }
}
```

---

### 6.3 MCP 协议集成

#### 什么是 MCP

**Model Context Protocol (MCP)** 是标准化的工具和资源接口，允许 Agent 安全地访问外部数据源和工具。

#### MCP 服务器示例

```json
{
  "mcp": {
    "servers": {
      "filesystem": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/user/projects"],
        "enabled": true
      },
      "github": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-github"],
        "env": {
          "GITHUB_TOKEN": "ghp_..."
        },
        "enabled": true
      },
      "postgres": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://localhost/mydb"],
        "enabled": false
      }
    }
  }
}
```

---

### 6.4 子 Agent 与任务分发

#### 子 Agent 配置

```json
{
  "agents": {
    "ceo": {
      "model": "anthropic/claude-opus-4",
      "subAgents": ["researcher", "writer", "coder", "reviewer"],
      "orchestration": "sequential"
    },
    "researcher": {
      "model": "anthropic/claude-sonnet-4",
      "tools": ["web_search", "web_fetch"],
      "output": "research_report"
    },
    "writer": {
      "model": "anthropic/claude-sonnet-4",
      "input": ["research_report"],
      "tools": ["file_ops"],
      "output": "draft"
    },
    "reviewer": {
      "model": "anthropic/claude-opus-4",
      "input": ["draft"],
      "output": "final"
    }
  }
}
```

---

### 6.5 定时任务与自动化

#### Cron 风格定时任务

```json
{
  "automation": {
    "tasks": [
      {
        "name": "daily-report",
        "schedule": "0 8 * * *",
        "agent": "analyst",
        "prompt": "生成昨日数据报告",
        "channel": "telegram",
        "recipient": "123456789"
      },
      {
        "name": "health-check",
        "schedule": "*/30 * * * *",
        "agent": "monitor",
        "prompt": "检查服务器状态",
        "onFailure": {
          "notify": "telegram",
          "recipient": "123456789"
        }
      }
    ]
  }
}
```

---

## 第七部分：会话与记忆管理

### 7.1 会话管理深度解析

#### Session Key vs Session ID

| 概念 | 描述 | 格式 |
|------|------|------|
| **Session ID** | 唯一会话标识符 | UUID (如 `550e8400-e29b-41d4-a716-446655440000`) |
| **Session Key** | 渠道 + 用户组合键 | `telegram:123456789` |

#### 会话状态机

```
[New] → [Active] → [Idle] → [Compacted] → [Archived] → [Deleted]
   │         │          │            │            │
   │         │          │            │            └─ 超过保留期
   │         │          │            └─ 30 天未使用
   │         │          └─ 上下文 > 80%
   │         └─ 用户交互
   └─ 首次消息
```

---

### 7.2 记忆系统架构

#### 记忆层级

```
┌─────────────────────────────────────────┐
│           Working Memory                │  ← 当前会话上下文
├─────────────────────────────────────────┤
│           Short-term Memory             │  ← 最近 N 次会话
├─────────────────────────────────────────┤
│           Long-term Memory              │  ← 持久化存储
│  ┌──────────────┐  ┌──────────────┐    │
│  │  Semantic    │  │  Keyword     │    │
│  │  Index       │  │  Index       │    │
│  └──────────────┘  └──────────────┘    │
└─────────────────────────────────────────┘
```

#### 记忆文件格式

```json
{
  "memory": {
    "entries": [
      {
        "id": "mem_123",
        "content": "用户偏好使用 Python 进行数据分析",
        "tags": ["preference", "python", "data"],
        "createdAt": "2026-03-22T10:30:00Z",
        "accessCount": 15,
        "lastAccessed": "2026-03-22T15:45:00Z"
      }
    ],
    "config": {
      "maxEntries": 1000,
      "semanticSearch": true,
      "autoExpire": true,
      "expireDays": 90
    }
  }
}
```

---

### 7.3 会话压缩机制

#### 压缩算法对比

| 算法 | 压缩率 | 速度 | 质量 | 适用场景 |
|------|--------|------|------|---------|
| **Summarize** | 70-90% | 慢 | 高 | 重要对话 |
| **Truncate** | 50-70% | 快 | 中 | 快速压缩 |
| **Extract** | 60-80% | 中 | 高 | 关键信息保留 |
| **Hybrid** | 70-85% | 中 | 高 | 通用场景 |

#### 压缩触发配置

```json
{
  "compaction": {
    "enabled": true,
    "triggers": {
      "tokenThreshold": 0.8,
      "messageCount": 100,
      "sessionAge": 86400
    },
    "strategy": {
      "method": "hybrid",
      "preserveSystemPrompt": true,
      "preserveLastN": 10,
      "summaryModel": "anthropic/claude-haiku-3"
    }
  }
}
```

---

### 7.4 会话清理与维护

#### 自动清理策略

```json
{
  "sessionManagement": {
    "cleanup": {
      "enabled": true,
      "schedule": "0 3 * * *",
      "rules": [
        {
          "condition": "age > 30d",
          "action": "archive"
        },
        {
          "condition": "age > 90d AND archived",
          "action": "delete"
        },
        {
          "condition": "size > 100MB",
          "action": "compact"
        }
      ]
    }
  }
}
```

#### 手动清理命令

```bash
# 清理过期会话
openclaw session cleanup --dry-run

# 执行清理
openclaw session cleanup --execute

# 归档旧会话
openclaw session archive --older-than 30d

# 删除已归档会话
openclaw session delete --archived --older-than 90d
```

---

## 第八部分：运维与安全

### 8.1 Gateway 运维管理

#### Gateway 生命周期管理

```bash
# 启动 Gateway
openclaw gateway start

# 停止 Gateway
openclaw gateway stop

# 重启 Gateway
openclaw gateway restart

# 查看状态
openclaw gateway status

# 查看日志
openclaw logs --follow

# 健康检查
openclaw health
```

#### systemd 服务管理

```bash
# 启用开机自启
sudo systemctl enable openclaw

# 启动服务
sudo systemctl start openclaw

# 停止服务
sudo systemctl stop openclaw

# 重启服务
sudo systemctl restart openclaw

# 查看状态
sudo systemctl status openclaw

# 查看日志
sudo journalctl -u openclaw -f
```

---

### 8.2 日志与调试

#### 日志级别

| 级别 | 描述 | 使用场景 |
|------|------|---------|
| **ERROR** | 错误 | 生产环境默认 |
| **WARN** | 警告 | 生产环境调试 |
| **INFO** | 信息 | 开发环境 |
| **DEBUG** | 调试 | 深度调试 |
| **TRACE** | 追踪 | 性能分析 |

#### 日志配置

```json
{
  "logging": {
    "level": "info",
    "format": "json",
    "output": {
      "console": true,
      "file": true,
      "syslog": false
    },
    "file": {
      "path": "/var/log/openclaw/openclaw.log",
      "maxSize": "100MB",
      "maxFiles": 10,
      "compress": true
    }
  }
}
```

#### 调试模式

```bash
# 启用调试模式
export DEBUG=openclaw:*
openclaw gateway

# 或修改配置
openclaw config set logging.level debug
```

---

### 8.3 监控与告警

#### Prometheus 指标

```yaml
# Prometheus 配置
scrape_configs:
  - job_name: 'openclaw'
    static_configs:
      - targets: ['localhost:8080']
    metrics_path: '/metrics'
```

#### 关键指标

| 指标 | 描述 | 告警阈值 |
|------|------|---------|
| `gateway_requests_total` | 总请求数 | - |
| `gateway_request_duration_seconds` | 请求延迟 | p99 > 5s |
| `gateway_active_sessions` | 活跃会话数 | > 1000 |
| `model_api_errors_total` | 模型 API 错误 | > 10/min |
| `memory_usage_bytes` | 内存使用 | > 80% |
| `token_usage_total` | Token 使用量 | - |

---

### 8.4 备份与恢复

#### 备份策略

```bash
#!/bin/bash
# /usr/local/bin/openclaw-backup.sh

BACKUP_DIR="/backup/openclaw"
DATE=$(date +%Y%m%d_%H%M%S)

# 备份配置
tar -czf $BACKUP_DIR/config_$DATE.tar.gz /etc/openclaw/

# 备份数据
tar -czf $BACKUP_DIR/data_$DATE.tar.gz /var/lib/openclaw/

# 备份记忆
tar -czf $BACKUP_DIR/memory_$DATE.tar.gz ~/.openclaw/memory/

# 清理旧备份（保留 7 天）
find $BACKUP_DIR -name "*.tar.gz" -mtime +7 -delete

echo "Backup completed: $DATE"
```

#### 恢复流程

```bash
# 停止服务
sudo systemctl stop openclaw

# 恢复配置
tar -xzf config_20260322_120000.tar.gz -C /

# 恢复数据
tar -xzf data_20260322_120000.tar.gz -C /

# 启动服务
sudo systemctl start openclaw
```

---

### 8.5 安全配置

#### API Key 管理

```bash
# 生成安全 Token
openssl rand -hex 32

# 存储到环境变量
export OPENCLAW_AUTH_TOKEN="your-secret-token"

# 或使用密钥管理服务
# AWS Secrets Manager / HashiCorp Vault
```

#### 访问控制列表

```json
{
  "security": {
    "accessControl": {
      "allowedIPs": ["192.168.1.0/24", "10.0.0.0/8"],
      "blockedIPs": ["203.0.113.0/24"],
      "requireAuth": true,
      "authMethods": ["token", "oauth"],
      "rateLimit": {
        "requestsPerMinute": 60,
        "requestsPerHour": 1000
      }
    }
  }
}
```

#### 审计日志

```json
{
  "security": {
    "audit": {
      "enabled": true,
      "logAuthAttempts": true,
      "logConfigChanges": true,
      "logDataAccess": true,
      "retention": 90
    }
  }
}
```

---

### 8.6 性能优化

#### 性能调优参数

```json
{
  "performance": {
    "gateway": {
      "maxConnections": 1000,
      "connectionTimeout": 30,
      "keepAlive": true
    },
    "memory": {
      "cacheSize": 1000,
      "indexBatchSize": 100
    },
    "model": {
      "maxConcurrent": 10,
      "requestTimeout": 120,
      "retryOnRateLimit": true
    }
  }
}
```

#### 资源监控

```bash
# 查看资源使用
openclaw status --verbose

# 性能分析
openclaw profile --duration 60

# 内存分析
openclaw memory stats
```

---

## 第九部分：故障排查与 FAQ

### 9.1 诊断命令速查

#### 快速诊断（前 60 秒）

```bash
# 1. 快速状态检查
openclaw status

# 2. 详细报告（可分享）
openclaw status --all

# 3. Gateway 状态
openclaw gateway status

# 4. 深度探测
openclaw status --deep

# 5. 查看日志
openclaw logs --follow

# 6. 运行诊断修复
openclaw doctor
```

#### 深度诊断

```bash
# Gateway 健康快照
openclaw health --json
openclaw health --verbose

# 模型连接测试
openclaw models test

# 渠道连接测试
openclaw channels test telegram

# 配置文件验证
openclaw config validate
```

---

### 9.2 高频问题解决方案

#### 问题 1：Gateway 无法启动

```bash
# 检查端口占用
lsof -i :8080
netstat -tlnp | grep 8080

# 杀掉占用进程
kill -9 <PID>

# 查看错误日志
openclaw logs --tail 100

# 常见错误：
# - "Address already in use": 端口被占用
# - "Config not found": 配置文件路径错误
# - "Permission denied": 权限不足
```

#### 问题 2：渠道连接失败

```bash
# 检查渠道配置
openclaw config get channels.telegram

# 测试渠道连接
openclaw channels test telegram

# 查看渠道日志
openclaw logs --grep telegram

# 常见错误：
# - "Invalid bot token": Token 错误
# - "Webhook verification failed": Webhook URL 不可达
# - "Rate limited": 请求过于频繁
```

#### 问题 3：模型 API 调用失败

```bash
# 检查模型配置
openclaw models list
openclaw models current

# 测试模型连接
openclaw models test anthropic/claude-sonnet-4

# 查看 API Key
echo $ANTHROPIC_API_KEY

# 常见错误：
# - "Invalid API key": API Key 错误/过期
# - "Rate limit exceeded": 超出速率限制
# - "Insufficient quota": 余额不足
```

#### 问题 4：上下文过大错误

```bash
# 压缩当前会话
openclaw session compact

# 重置会话
openclaw session reset

# 调整压缩阈值
openclaw config set compaction.threshold 0.7

# 预防措施：
# - 定期使用 /new 命令新建会话
# - 启用自动压缩
# - 限制历史消息数量
```

#### 问题 5：内存使用过高

```bash
# 查看内存统计
openclaw memory stats

# 清理记忆缓存
openclaw memory clear

# 限制记忆大小
openclaw config set memory.maxSize 500

# 重启 Gateway（释放内存）
openclaw gateway restart
```

---

### 9.3 FAQ（50+ 常见问题）

#### 安装与配置

**Q: 安装时遇到 npm ERR! 怎么办？**  
A: 尝试使用国内镜像：`npm config set registry https://registry.npmmirror.com`

**Q: Windows 安装后命令不可用？**  
A: 重启终端或添加 npm 全局路径到 PATH：`C:\Users\<user>\AppData\Roaming\npm`

**Q: 如何迁移配置到新机器？**  
A: 复制 `~/.openclaw/` 目录到新机器，保持目录结构不变

#### 渠道相关

**Q: Telegram Bot 不回复？**  
A: 检查：1) Bot Token 正确 2) 用户 ID 在 allowFrom 列表 3) Gateway 正在运行

**Q: WhatsApp 无法连接群组？**  
A: 需要获取群组 JID（格式：`1234567890-1234567890@g.us`），并在配置中添加

**Q: Discord Bot 无法读取消息？**  
A: 启用 Privileged Gateway Intents（MESSAGE CONTENT INTENT）

#### 模型相关

**Q: 如何切换模型？**  
A: `openclaw model use anthropic/claude-opus-4`

**Q: 所有模型都失败怎么办？**  
A: 检查网络连接、API Key 有效性、查看 `openclaw status --deep`

**Q: 本地模型响应慢？**  
A: 使用更小模型（如 llama3.2:3b）、增加 GPU、使用量化版本

#### 会话与记忆

**Q: 如何开始新对话？**  
A: 发送 `/new` 命令或 `openclaw session reset`

**Q: 记忆能保存多久？**  
A: 默认永久保存，可配置自动过期（如 90 天）

**Q: 如何搜索记忆？**  
A: 自动语义搜索，无需手动操作

#### 性能与优化

**Q: 如何降低 Token 成本？**  
A: 使用 Haiku 等轻量模型、启用压缩、缓存常用回复

**Q: Gateway 占用内存过高？**  
A: 限制记忆大小、定期清理、增加 swap 空间

**Q: 响应延迟高？**  
A: 选择就近的模型提供商、使用更快的模型、优化网络

#### 安全与隐私

**Q: 数据是否安全？**  
A: 所有数据本地存储，可配置加密、访问控制

**Q: 如何防止未授权访问？**  
A: 配置 allowFrom、使用 Token 认证、启用 IP 白名单

**Q: 日志是否包含敏感信息？**  
A: API Key 等敏感信息会自动脱敏

---

### 9.4 开发者支持

#### 本地开发环境

```bash
# 克隆源码
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# 安装依赖
npm install

# 开发模式运行
npm run dev

# 运行测试
npm test
```

#### 贡献指南

1. Fork 仓库
2. 创建功能分支：`git checkout -b feature/my-feature`
3. 提交更改：`git commit -am 'Add new feature'`
4. 推送到分支：`git push origin feature/my-feature`
5. 创建 Pull Request

#### 获取帮助

- **文档**: https://docs.openclaw.ai/
- **GitHub Issues**: https://github.com/openclaw/openclaw/issues
- **Discord**: https://discord.com/invite/clawd
- **邮件**: support@openclaw.ai

---

## 附录

### 附录 A：环境变量参考

| 变量名 | 描述 | 默认值 | 示例 |
|--------|------|--------|------|
| `OPENCLAW_CONFIG_PATH` | 配置文件路径 | `~/.openclaw/config.json` | `/etc/openclaw/config.json` |
| `OPENCLAW_DATA_DIR` | 数据目录 | `~/.openclaw/data` | `/var/lib/openclaw` |
| `OPENCLAW_LOG_LEVEL` | 日志级别 | `info` | `debug` |
| `ANTHROPIC_API_KEY` | Anthropic API Key | - | `sk-ant-...` |
| `OPENAI_API_KEY` | OpenAI API Key | - | `sk-...` |
| `GOOGLE_API_KEY` | Google API Key | - | `AIza...` |
| `DEBUG` | 调试模式 | - | `openclaw:*` |
| `NODE_ENV` | Node 环境 | `development` | `production` |

---

### 附录 B：配置文件完整参考

```json
{
  "gateway": {
    "port": 8080,
    "bind": "0.0.0.0",
    "cors": { "enabled": true, "origins": [] },
    "auth": { "token": "", "allowFrom": [] }
  },
  "dashboard": {
    "port": 3000,
    "enabled": true
  },
  "models": {
    "default": "anthropic/claude-sonnet-4",
    "providers": {},
    "aliases": {},
    "failover": { "enabled": true, "fallbackChain": [] }
  },
  "channels": {},
  "agents": {
    "default": {
      "model": "",
      "systemPrompt": "",
      "skills": [],
      "memory": { "enabled": true },
      "context": { "maxTokens": 8192 }
    }
  },
  "memory": {
    "enabled": true,
    "maxSize": 1000,
    "semanticSearch": true
  },
  "tools": {},
  "logging": {
    "level": "info",
    "format": "json",
    "output": { "console": true, "file": true }
  },
  "security": {
    "accessControl": {},
    "audit": { "enabled": true }
  },
  "performance": {},
  "automation": { "tasks": [] }
}
```

---

### 附录 C：CLI 命令参考

#### Gateway 命令

```bash
openclaw gateway start|stop|restart|status
openclaw health [--json|--verbose]
openclaw logs [--follow|--tail N]
```

#### 模型命令

```bash
openclaw model list|current|use|default
openclaw models test [model-name]
openclaw usage tokens [--by-model|--by-channel]
```

#### 会话命令

```bash
openclaw session list|get|delete|purge
openclaw session compact|reset|export
openclaw session cleanup [--dry-run|--execute]
```

#### 渠道命令

```bash
openclaw channels list|test|enable|disable
openclaw channel config <channel-name>
```

#### 配置命令

```bash
openclaw config get|set|validate|export|import
openclaw doctor
openclaw status [--all|--deep|--verbose]
```

---

### 附录 D：目录结构与文件位置

```
~/.openclaw/
├── config.json              # 主配置文件
├── workspaces/
│   ├── default/
│   │   ├── AGENTS.md
│   │   ├── SOUL.md
│   │   ├── MEMORY.md
│   │   ├── skills/
│   │   └── memory/
│   └── ...
├── data/
│   ├── sessions/
│   ├── memory/
│   └── cache/
├── logs/
│   ├── openclaw.log
│   └── openclaw.log.1.gz
└── tmp/
    └── ...

/etc/openclaw/              # 系统级配置（生产环境）
├── config.json
└── systemd/
    └── openclaw.service

/var/lib/openclaw/          # 系统级数据（生产环境）
├── data/
├── memory/
└── logs/
```

---

## 📝 许可证

本文档采用 **MIT 许可证**。您可以自由使用、修改和分发，但需保留原始版权声明。

---

## 🔗 相关链接

- **OpenClaw 官网**: https://openclaw.ai/
- **官方文档**: https://docs.openclaw.ai/
- **GitHub 仓库**: https://github.com/openclaw/openclaw
- **Discord 社区**: https://discord.com/invite/clawd
- **npm 包**: https://www.npmjs.com/package/openclaw
- **Docker 镜像**: https://hub.docker.com/r/openclaw/openclaw

---

**文档版本**: v2026.03.23  
**最后更新**: 2026-03-23  
**基于官方文档版本**: 2026-03-22  
**文档大小**: ~50KB, 2000+ 行  
**章节数**: 9 大部分 + 4 附录，50+ 子章节  
**代码示例**: 100+ 个  
**表格**: 30+ 个
