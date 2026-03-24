# OpenClaw CLI 命令完全手册 🦞💻

**版本**: v1.0 (2026-03-24)  
**来源**: 提取自 [openclaw.md](https://github.com/hjs2015/ai-coder/blob/main/docs/openclaw.md) 第三部分  
**OpenClaw 版本**: 2026.3.23-1  
**命令数量**: 38 个（13 大类）

---

## 📑 目录

- [全局选项](#全局选项)
- [完整命令列表](#完整命令列表 38 个)
- [基础命令](#基础命令)
- [Agent 管理](#agent-管理)
- [渠道管理](#渠道管理)
- [配置管理](#配置管理)
- [会话管理](#会话管理)
- [记忆管理](#记忆管理)
- [性能监控](#性能监控)
- [备份恢复](#备份恢复)
- [安全权限](#安全权限)
- [插件管理](#插件管理)
- [开发调试](#开发调试)
- [系统维护](#系统维护)
- [使用示例](#使用示例)

---

## 全局选项

```bash
# 开发模式（隔离状态，端口 19001）
openclaw --dev

# 使用命名 profile（隔离配置）
openclaw --profile <name>

# 设置日志级别
openclaw --log-level <level>
# 可选值：silent|fatal|error|warn|info|debug|trace

# 禁用颜色输出
openclaw --no-color

# 查看版本
openclaw -V, --version

# 查看帮助
openclaw -h, --help
```

---

## 完整命令列表（38 个）

**带 * 的命令有子命令**，运行 `<command> --help` 查看详情。

| 命令 | 说明 | 类别 |
|------|------|------|
| `acp *` | Agent Control Protocol 工具 | Agent |
| `agent` | 通过 Gateway 运行单个 agent 轮次 | Agent |
| `agents *` | 管理独立的 agents（工作空间、认证、路由） | Agent |
| `approvals *` | 管理执行审批（gateway 或 node 主机） | 安全 |
| `backup *` | 创建和验证 OpenClaw 状态备份 | 运维 |
| `browser *` | 管理专用浏览器（Chrome/Chromium） | 工具 |
| `channels *` | 管理连接的聊天渠道 | 渠道 |
| `clawbot *` | 传统 clawbot 命令别名 | 兼容 |
| `completion` | 生成 shell 自动补全脚本 | 工具 |
| `config *` | 非交互式配置助手 | 配置 |
| `configure` | 交互式配置（凭证、渠道、gateway、agent 默认值） | 配置 |
| `cron *` | 通过 Gateway 调度器管理 cron 任务 | 调度 |
| `daemon *` | Gateway 服务（传统别名） | 兼容 |
| `dashboard` | 打开 Dashboard | 运维 |
| `debug *` | 调试模式控制 | 开发 |
| `deploy *` | 部署命令（Docker、systemd） | 运维 |
| `doctor` | 诊断工具 | 运维 |
| `embeddings *` | 管理嵌入模型和向量数据库 | 记忆 |
| `gateway *` | Gateway 服务控制 | 运维 |
| `init` | 初始化工作空间 | 配置 |
| `knowledge *` | 管理知识库（RAG） | 记忆 |
| `logs` | 查看日志 | 运维 |
| `mcp *` | MCP 服务器管理 | 工具 |
| `memory *` | 管理长期记忆存储 | 记忆 |
| `models *` | 管理 AI 模型配置 | 配置 |
| `node *` | 管理计算节点 | 运维 |
| `plugin *` | 插件管理 | 插件 |
| `restore *` | 从备份恢复 | 运维 |
| `run` | 运行 OpenClaw 服务 | 运维 |
| `schedule *` | 管理调度任务 | 调度 |
| `secrets *` | 管理密钥存储 | 安全 |
| `security *` | 安全管理 | 安全 |
| `session *` | 管理会话历史 | 会话 |
| `skill *` | 管理技能 | 插件 |
| `skills *` | 管理技能（别名） | 插件 |
| `stats` | 查看统计信息 | 监控 |
| `tools *` | 管理工具配置 | 工具 |
| `user *` | 用户管理 | 安全 |

---

## 基础命令

### openclaw start

启动 OpenClaw 服务

```bash
# 前台启动
openclaw start

# 后台启动
openclaw start --daemon

# 指定配置文件
openclaw start --config /path/to/openclaw.json

# 指定端口
openclaw start --port 19001
```

---

### openclaw stop

停止 OpenClaw 服务

```bash
# 正常停止
openclaw stop

# 强制停止
openclaw stop --force
```

---

### openclaw restart

重启 OpenClaw 服务

```bash
# 重启
openclaw restart

# 重启并指定端口
openclaw restart --port 19001
```

---

### openclaw status

查看服务状态

```bash
openclaw status
# 输出：
# OpenClaw Status
# ├─ Status: running
# ├─ PID: 12345
# ├─ Port: 18789
# ├─ Uptime: 2d 5h 30m
# └─ Memory: 256MB
```

---

### openclaw version

查看版本信息

```bash
openclaw version
# 输出：
# OpenClaw v2026.3.23-1
# Node.js: v22.16+
# OS: Linux 5.15.0-ubuntu
# Build: 2026-03-23
```

---

### openclaw info

系统信息

```bash
openclaw info
# 输出：
# OpenClaw System Info
# ├─ Version: 2026.3.23-1
# ├─ Node.js: v22.16+
# ├─ npm: 10.2.4
# ├─ OS: Linux 5.15.0-ubuntu
# ├─ Arch: x64
# ├─ Memory: 8GB (4.2GB free)
# ├─ Disk: 500GB (234GB free)
# ├─ CPU: 4 cores
# └─ Uptime: 2d 5h 30m
```

---

### openclaw init

初始化工作空间

```bash
# 交互式初始化
openclaw init

# 快速初始化（使用默认配置）
openclaw init --quick

# 指定工作空间目录
openclaw init /path/to/workspace
```

---

## Agent 管理

### openclaw agent run

运行单个 Agent 轮次

```bash
# 运行默认 Agent
openclaw agent run

# 指定 Agent
openclaw agent run coding-agent

# 指定消息
openclaw agent run coding-agent --message "帮我写一个 Python 脚本"

# 指定模型
openclaw agent run coding-agent --model qwen-max
```

**输出示例**：
```
Running agent: coding-agent
Model: qwen-max
───────────────────────────────────────
User: 帮我写一个 Python 脚本
Assistant: 好的，这是一个简单的 Python 脚本...
───────────────────────────────────────
Tokens used: 234
Cost: ¥0.01
Time: 1.2s
```

---

### openclaw agents list

列出所有 Agent

```bash
# 列出所有 Agent
openclaw agents list

# 显示详细信息
openclaw agents list --verbose

# 按状态过滤
openclaw agents list --status active
```

**输出示例**：
```
Available Agents
├─ default
│  ├─ Model: qwen-max
│  ├─ System: "你是一个有用的助手"
│  ├─ Tools: none
│  └─ Status: active
├─ coding-agent
│  ├─ Model: qwen-max
│  ├─ System: "你是一个专业的编程助手"
│  ├─ Tools: code-interpreter,file-reader
│  └─ Status: active
└─ data-analyst
   ├─ Model: ernie-4.0
   ├─ System: "你是一个数据分析专家"
   ├─ Tools: python-reinterpreter,chart-generator
   └─ Status: inactive
```

---

### openclaw agents show

查看 Agent 详情

```bash
openclaw agents show coding-agent

# 显示完整配置
openclaw agents show coding-agent --full
```

**输出示例**：
```
Agent Details: coding-agent
───────────────────────────────────────
Name: coding-agent
Model: qwen-max
System Prompt: "你是一个专业的编程助手"
Tools:
  ├─ code-interpreter
  └─ file-reader
Workspace: /root/.openclaw/workspaces/coding-agent
Auth: none
Routing: default
Status: active
Created: 2026-03-20 10:30:00
Last Modified: 2026-03-23 14:25:00
───────────────────────────────────────
```

---

### openclaw agent create

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

### openclaw agent edit

编辑 Agent 配置

```bash
openclaw agent edit coding-agent
# 打开编辑器修改配置
```

---

### openclaw agent remove

删除 Agent

```bash
openclaw agent remove coding-agent

# 强制删除
openclaw agent remove coding-agent --force
```

---

## 配置管理

### openclaw config（无子命令）

启动引导式配置向导

```bash
openclaw config
# 或指定配置部分
openclaw config --section channel
openclaw config --section model
```

**说明**：
- 无子命令时启动交互式配置向导
- 可通过 `--section` 指定配置部分
- 适合新手首次配置

---

### openclaw config file

打印活动配置文件路径

```bash
openclaw config file
# 输出示例：
# /root/.openclaw/openclaw.json
```

---

### openclaw config get

获取配置项的值（通过点路径）

**基本语法**：
```bash
openclaw config get <配置键>
```

**常用命令**：
```bash
# 查看工具权限配置
openclaw config get tools.profile

# 查看默认模型
openclaw config get models

# 查看网关端口
openclaw config get gateway.port

# 查看特定渠道配置
openclaw config get channels.feishu

# 查看 Agent 配置
openclaw config get agents
```

**输出示例**：
```
tools.profile: messaging
gateway.port: 18789
models.default: qwen-max
```

---

### openclaw config set

设置配置项的值

**基本语法**：
```bash
openclaw config set <配置键> <值>
```

**常用命令**：

**1. 解锁完整工具权限（重要）⭐⭐⭐**
```bash
# 解锁完整工具权限（允许执行命令、文件操作、代码运行等）
openclaw config set tools.profile full

# 仅开放消息相关权限（默认，只能聊天）
openclaw config set tools.profile messaging

# 自定义工具权限
openclaw config set tools.profile custom
```

**2. 配置默认模型**
```bash
# 设置默认使用的 AI 模型
openclaw config set models.default qwen-max

# 设置为通义千问
openclaw config set models.default qwen-max

# 设置为文心一言
openclaw config set models.default ernie-4.0

# 设置为豆包
openclaw config set models.default doubao-pro
```

**3. 配置网关端口**
```bash
# 设置网关端口（默认 18789）
openclaw config set gateway.port 18789

# 自定义端口
openclaw config set gateway.port 19001
```

**4. 配置 Agent**
```bash
# 设置默认 Agent
openclaw config set agents.default coding-agent

# 配置 Agent 使用的模型
openclaw config set agents.coding-agent.model qwen-max
```

**5. 配置渠道**
```bash
# 启用/禁用渠道
openclaw config set channels.feishu.enabled true
openclaw config set channels.telegram.enabled false
```

**6. 配置安全设置**
```bash
# 启用 DM（直接消息）策略
openclaw config set security.dm_policy allow

# 设置 TCC（工具调用控制）权限
openclaw config set security.tcc.enabled true
```

**高级用法**：

**引用提供者模式**（推荐用于敏感信息）：
```bash
# 设置渠道 Token（从环境变量读取）
openclaw config set channels.discord.token --ref-provider default --ref-source env --ref-id DISCORD_BOT_TOKEN

# 设置密钥提供者
openclaw config set secrets.providers.vault --provider-source file --provider-path /etc/openclaw/secrets.json --provider-mode json
```

**批量设置模式**：
```bash
# 从批量文件设置（先 dry-run 预览）
openclaw config set --batch-file ./config-set.batch.json --dry-run

# 实际执行
openclaw config set --batch-file ./config-set.batch.json
```

**严格 JSON 模式**：
```bash
openclaw config set gateway.port 19001 --strict-json
```

**输出示例**：
```
✓ Configuration updated successfully
✓ tools.profile: messaging → full
✓ Gateway will restart to apply changes
```

---

### openclaw config unset

移除配置项

```bash
# 移除特定配置
openclaw config unset tools.profile
openclaw config unset models.default

# 移除渠道配置
openclaw config unset channels.telegram
```

**说明**：
- 删除后该配置项恢复默认值或不存在
- 敏感信息建议使用此命令清除

---

### openclaw config validate

验证配置文件

```bash
openclaw config validate
# 输出：
# ✓ Configuration file is valid
# ✓ All channels configured correctly
# ✓ All models have valid API keys
# ✓ All agents reference existing models
```

**验证内容**：
- ✅ 配置文件格式是否正确
- ✅ 所有渠道配置是否完整
- ✅ 所有模型 API Key 是否有效
- ✅ 所有 Agent 引用的模型是否存在

---

## 会话管理

### openclaw session list

列出所有会话

```bash
# 列出所有会话
openclaw session list

# 按渠道过滤
openclaw session list --channel feishu

# 按用户过滤
openclaw session list --user ou_xxx

# 显示最近活跃时间
openclaw session list --sort-by last_active

# 限制数量
openclaw session list --limit 20
```

**输出示例**：
```
Active Sessions
├─ sess_abc123
│  ├─ User: ou_xxx
│  ├─ Channel: feishu
│  ├─ Messages: 45
│  ├─ Created: 2026-03-20 09:30
│  └─ Last Active: 2026-03-23 14:25
├─ sess_def456
│  ├─ User: tg_user123
│  ├─ Channel: telegram
│  ├─ Messages: 12
│  ├─ Created: 2026-03-22 16:45
│  └─ Last Active: 2026-03-23 14:20
└─ sess_ghi789
   ├─ User: wx_user456
   ├─ Channel: wechat
   ├─ Messages: 89
   ├─ Created: 2026-03-18 10:00
   └─ Last Active: 2026-03-23 14:15
```

---

### openclaw session show

查看会话详情

```bash
openclaw session show sess_abc123

# 显示消息历史
openclaw session show sess_abc123 --with-messages

# 限制消息数量
openclaw session show sess_abc123 --with-messages --limit 10
```

**输出示例**：
```
Session Details
───────────────────────────────────────
Session ID: sess_abc123
User ID: ou_xxx
Channel: feishu
Agent: default
Model: qwen-max
Messages: 45
Tokens Used: 12,345
Created: 2026-03-20 09:30:15
Last Active: 2026-03-23 14:25:30
───────────────────────────────────────

Recent Messages:
[09:30] 用户：你好
[09:30] AI: 你好！有什么我可以帮助你的吗？
[09:31] 用户：帮我写一个 Python 脚本
[09:31] AI: 好的，请问你需要什么功能的脚本？
...
```

---

### openclaw session clear

清空会话历史

```bash
# 清空指定会话
openclaw session clear sess_abc123

# 清空所有会话（需要确认）
openclaw session clear --all

# 强制清空（跳过确认）
openclaw session clear --all --force

# 清空特定渠道的会话
openclaw session clear --channel feishu
```

---

### openclaw session export

导出会话

```bash
# 导出为 JSON
openclaw session export sess_abc123

# 导出为文本
openclaw session export sess_abc123 --format txt

# 导出为 Markdown
openclaw session export sess_abc123 --format md

# 导出到文件
openclaw session export sess_abc123 --output conversation.md
```

---

### openclaw session delete

删除会话

```bash
# 删除指定会话
openclaw session delete sess_abc123

# 删除所有会话（危险操作）
openclaw session delete --all

# 删除 7 天前的会话
openclaw session delete --older-than 7d

# 删除特定渠道的会话
openclaw session delete --channel telegram
```

---

## 记忆管理

### openclaw memory add

添加记忆

```bash
# 添加文本记忆
openclaw memory add "用户偏好使用 Python 进行数据分析"

# 添加文件记忆
openclaw memory add --file document.pdf

# 添加 URL 记忆
openclaw memory add --url https://example.com/article

# 指定集合
openclaw memory add "重要信息" --collection personal
```

---

### openclaw memory search

搜索记忆

```bash
# 语义搜索
openclaw memory search "Python 数据分析"

# 限制结果数量
openclaw memory search "Python" --limit 5

# 指定集合
openclaw memory search "Python" --collection personal

# 显示相似度
openclaw memory search "Python" --show-score

# 最小相似度阈值
openclaw memory search "Python" --min-score 0.7
```

**输出示例**：
```
Memory Search Results: "Python 数据分析"
────────────────────────────────────────────
[0.92] 用户偏好使用 Python 进行数据分析
       Collection: personal | Added: 2026-03-20

[0.85] Python pandas 库适合处理表格数据
       Collection: knowledge | Added: 2026-03-21

[0.78] 推荐使用 Jupyter Notebook 进行探索性分析
       Collection: knowledge | Added: 2026-03-22
```

---

### openclaw memory list

列出记忆集合

```bash
# 列出所有集合
openclaw memory list

# 查看集合详情
openclaw memory list --collection personal

# 显示统计信息
openclaw memory list --stats
```

**输出示例**：
```
Memory Collections
├─ default
│  ├─ Items: 156
│  ├─ Size: 2.3MB
│  └─ Last Updated: 2026-03-23 14:00
├─ personal
│  ├─ Items: 23
│  ├─ Size: 0.5MB
│  └─ Last Updated: 2026-03-22 18:30
└─ knowledge
   ├─ Items: 89
   ├─ Size: 1.8MB
   └─ Last Updated: 2026-03-23 12:15
```

---

### openclaw memory clear

清空记忆

```bash
# 清空指定集合
openclaw memory clear --collection personal

# 清空所有记忆（危险）
openclaw memory clear --all

# 强制清空
openclaw memory clear --all --force
```

---

## 性能监控

### openclaw stats

查看统计信息

```bash
# 查看总体统计
openclaw stats

# 查看今日统计
openclaw stats --today

# 查看最近 7 天统计
openclaw stats --days 7

# 查看实时统计
openclaw stats --live
```

**输出示例**：
```
OpenClaw Statistics (Last 7 Days)
────────────────────────────────────────────
Messages Processed: 1,234
Tokens Used: 456,789
  ├─ Input: 234,567
  └─ Output: 222,222

Active Users: 45
Active Sessions: 23
Active Channels: 3

Top Models:
  ├─ qwen-max: 678 messages (55%)
  ├─ ernie-4.0: 345 messages (28%)
  └─ doubao-pro: 211 messages (17%)

Cost Estimate: ¥18.45
Avg Response Time: 1.2s
────────────────────────────────────────────
```

---

### openclaw top

查看 TOP 排行榜

```bash
# 查看最活跃用户
openclaw top users

# 查看最活跃会话
openclaw top sessions

# 查看最常用模型
openclaw top models

# 查看最活跃渠道
openclaw top channels

# 限制数量
openclaw top users --limit 10
```

**输出示例**：
```
Top Users (Last 7 Days)
├─ 1. ou_xxx (Feishu) - 234 messages
├─ 2. tg_user123 (Telegram) - 189 messages
├─ 3. wx_user456 (WeChat) - 156 messages
├─ 4. ou_yyy (Feishu) - 134 messages
└─ 5. tg_user789 (Telegram) - 98 messages
```

---

### openclaw benchmark

性能基准测试

```bash
# 运行基准测试
openclaw benchmark

# 测试特定模型
openclaw benchmark --model qwen-max

# 测试所有模型
openclaw benchmark --all-models

# 输出详细报告
openclaw benchmark --verbose
```

**输出示例**：
```
Model Benchmark Results
────────────────────────────────────────────
Model: qwen-max
  ├─ First Token: 0.3s
  ├─ Total Time: 1.2s
  ├─ Tokens/sec: 45
  └─ Cost/1K: ¥0.04

Model: ernie-4.0
  ├─ First Token: 0.4s
  ├─ Total Time: 1.5s
  ├─ Tokens/sec: 38
  └─ Cost/1K: ¥0.03

Model: doubao-pro
  ├─ First Token: 0.2s
  ├─ Total Time: 0.9s
  ├─ Tokens/sec: 52
  └─ Cost/1K: ¥0.02
────────────────────────────────────────────
```

---

## 备份恢复

### openclaw backup

备份数据

```bash
# 创建备份
openclaw backup

# 备份到指定目录
openclaw backup --output /backup/openclaw

# 仅备份配置
openclaw backup --config-only

# 仅备份会话
openclaw backup --sessions-only

# 压缩备份
openclaw backup --compress
```

**输出示例**：
```
Creating backup...
✓ Configuration backed up
✓ Sessions backed up (23 sessions, 2.3MB)
✓ Memory backed up (268 items, 4.6MB)
✓ Logs backed up (7 days, 15MB)

Backup saved to: /backup/openclaw/backup_2026-03-23_14-30-00.tar.gz
Total size: 22.1MB
```

---

### openclaw restore

恢复数据

```bash
# 从备份恢复
openclaw restore /backup/openclaw/backup_2026-03-23_14-30-00.tar.gz

# 仅恢复配置
openclaw restore backup.tar.gz --config-only

# 仅恢复会话
openclaw restore backup.tar.gz --sessions-only

# 强制恢复（覆盖现有数据）
openclaw restore backup.tar.gz --force
```

---

### openclaw backup list

列出备份

```bash
openclaw backup list

# 显示详细信息
openclaw backup list --verbose

# 按时间排序
openclaw backup list --sort-by time
```

**输出示例**：
```
Available Backups
├─ backup_2026-03-23_14-30-00.tar.gz
│  ├─ Size: 22.1MB
│  ├─ Sessions: 23
│  └─ Memory Items: 268
├─ backup_2026-03-22_08-00-00.tar.gz
│  ├─ Size: 21.8MB
│  ├─ Sessions: 21
│  └─ Memory Items: 245
└─ backup_2026-03-21_08-00-00.tar.gz
   ├─ Size: 20.5MB
   ├─ Sessions: 19
   └─ Memory Items: 230
```

---

## 安全与权限

### openclaw user list

列出用户

```bash
openclaw user list

# 显示详细信息
openclaw user list --verbose

# 按渠道过滤
openclaw user list --channel feishu
```

---

### openclaw user grant

授予用户权限

```bash
# 授予管理员权限
openclaw user grant ou_xxx admin

# 授予开发者权限
openclaw user grant ou_xxx developer

# 授予普通用户权限
openclaw user grant ou_xxx user
```

---

### openclaw user revoke

撤销用户权限

```bash
# 撤销管理员权限
openclaw user revoke ou_xxx admin

# 撤销所有权限
openclaw user revoke ou_xxx --all
```

---

### openclaw user audit

审计用户操作

```bash
# 查看用户操作日志
openclaw user audit ou_xxx

# 查看最近 100 条操作
openclaw user audit ou_xxx --limit 100

# 查看特定操作类型
openclaw user audit ou_xxx --action config_change
```

---

## 插件管理

### openclaw plugin list

列出已安装插件

```bash
openclaw plugin list

# 显示详细信息
openclaw plugin list --verbose

# 查看可用插件
openclaw plugin list --available
```

**输出示例**：
```
Installed Plugins
├─ @openclaw/channel-wecom v1.0.0
├─ @openclaw/channel-dingtalk v1.0.0
├─ @openclaw/channel-wechaty v0.9.0
└─ @openclaw/skill-weather v1.2.0
```

---

### openclaw plugin install

安装插件

```bash
# 安装插件
openclaw plugin install @openclaw/channel-wecom

# 安装指定版本
openclaw plugin install @openclaw/channel-wecom@1.0.0

# 从文件安装
openclaw plugin install ./my-plugin.tar.gz
```

---

### openclaw plugin update

更新插件

```bash
# 更新所有插件
openclaw plugin update

# 更新特定插件
openclaw plugin update @openclaw/channel-wecom

# 检查可更新插件
openclaw plugin update --check
```

---

### openclaw plugin uninstall

卸载插件

```bash
openclaw plugin uninstall @openclaw/channel-wecom

# 强制卸载
openclaw plugin uninstall @openclaw/channel-wecom --force
```

---

## 开发调试

### openclaw logs

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

### openclaw doctor

诊断工具

```bash
openclaw doctor
# 输出：
# OpenClaw Doctor
#
# System
# ✓ Node.js v22.16+
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

### openclaw debug

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

### openclaw dashboard

打开 Dashboard

```bash
openclaw dashboard
# 输出：
# Opening dashboard at `--port` 配置的端口
# (自动打开默认浏览器)
```

**Dashboard 功能**：
- 实时监控消息流
- 查看会话历史
- 管理 Agent 配置
- 查看 Token 使用统计
- 查看成本分析

---

## 系统维护

### openclaw cleanup

清理临时文件

```bash
# 清理临时文件
openclaw cleanup

# 清理日志（保留最近 7 天）
openclaw cleanup --logs --keep-days 7

# 清理缓存
openclaw cleanup --cache

# 清理旧备份（保留最近 3 个）
openclaw cleanup --backups --keep-count 3
```

---

### openclaw optimize

优化性能

```bash
# 优化向量数据库
openclaw optimize

# 优化会话存储
openclaw optimize --sessions

# 优化记忆索引
openclaw optimize --memory

# 显示优化报告
openclaw optimize --verbose
```

---

### openclaw migrate

数据迁移

```bash
# 迁移数据到新版本
openclaw migrate

# 迁移特定数据
openclaw migrate --sessions
openclaw migrate --memory

# 回滚迁移
openclaw migrate --rollback
```

---

## 使用示例

### 示例 1：首次安装配置

```bash
# 1. 初始化工作空间
openclaw init --quick

# 2. 启动交互式配置
openclaw configure

# 3. 解锁完整工具权限
openclaw config set tools.profile full

# 4. 设置默认模型
openclaw config set models.default qwen-max

# 5. 启动服务
openclaw start --daemon

# 6. 验证服务状态
openclaw status
```

---

### 示例 2：配置飞书渠道

```bash
# 1. 设置飞书渠道配置
openclaw config set channels.feishu.appId cli_xxxxx
openclaw config set channels.feishu.appSecret xxxxxxx
openclaw config set channels.feishu.encryptKey xxxxxxx
openclaw config set channels.feishu.verificationToken xxxxxxx

# 2. 启用飞书渠道
openclaw config set channels.feishu.enabled true

# 3. 验证配置
openclaw config validate

# 4. 重启服务
openclaw restart

# 5. 查看日志确认连接
openclaw logs --channel feishu
```

---

### 示例 3：创建自定义 Agent

```bash
# 1. 创建编程助手 Agent
openclaw agent create coding-agent \
  --model qwen-max \
  --system-prompt "你是一个专业的编程助手，擅长 Python、JavaScript 和 Shell 脚本" \
  --tools code-interpreter,file-reader,web-search

# 2. 设置为默认 Agent
openclaw config set agents.default coding-agent

# 3. 测试 Agent
openclaw agent run coding-agent --message "帮我写一个 Python 脚本，实现文件批量重命名"

# 4. 查看会话历史
openclaw session show --with-messages --limit 10
```

---

### 示例 4：性能监控与优化

```bash
# 1. 查看统计信息
openclaw stats --days 7

# 2. 查看最活跃用户
openclaw top users --limit 10

# 3. 性能基准测试
openclaw benchmark --all-models

# 4. 优化向量数据库
openclaw optimize --memory

# 5. 清理旧数据
openclaw cleanup --logs --keep-days 7
openclaw cleanup --backups --keep-count 3
```

---

### 示例 5：备份与恢复

```bash
# 1. 创建备份
openclaw backup --compress --output /backup/openclaw

# 2. 列出备份
openclaw backup list

# 3. 验证备份
openclaw backup verify /backup/openclaw/backup_2026-03-23_14-30-00.tar.gz

# 4. 恢复数据（需要时）
openclaw restore /backup/openclaw/backup_2026-03-23_14-30-00.tar.gz --force
```

---

## 附录 A：命令速查表

### 基础命令（10 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `start` | 启动服务 | `openclaw start --daemon` |
| `stop` | 停止服务 | `openclaw stop` |
| `restart` | 重启服务 | `openclaw restart` |
| `status` | 查看状态 | `openclaw status` |
| `version` | 查看版本 | `openclaw version` |
| `info` | 系统信息 | `openclaw info` |
| `init` | 初始化 | `openclaw init --quick` |
| `run` | 运行服务 | `openclaw run` |
| `logs` | 查看日志 | `openclaw logs -f` |
| `doctor` | 诊断工具 | `openclaw doctor` |

### 配置命令（6 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `config` | 配置向导 | `openclaw config` |
| `config file` | 配置文件路径 | `openclaw config file` |
| `config get` | 获取配置 | `openclaw config get tools.profile` |
| `config set` | 设置配置 | `openclaw config set tools.profile full` |
| `config unset` | 移除配置 | `openclaw config unset channels.telegram` |
| `config validate` | 验证配置 | `openclaw config validate` |

### Agent 命令（5 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `agent run` | 运行 Agent | `openclaw agent run coding-agent` |
| `agents list` | 列出 Agent | `openclaw agents list` |
| `agents show` | 查看 Agent 详情 | `openclaw agents show coding-agent` |
| `agent create` | 创建 Agent | `openclaw agent create coding-agent` |
| `agent remove` | 删除 Agent | `openclaw agent remove coding-agent` |

### 会话命令（5 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `session list` | 列出会话 | `openclaw session list --limit 20` |
| `session show` | 查看会话 | `openclaw session show sess_abc123` |
| `session clear` | 清空会话 | `openclaw session clear --all` |
| `session export` | 导出会话 | `openclaw session export sess_abc123 --format md` |
| `session delete` | 删除会话 | `openclaw session delete sess_abc123` |

### 记忆命令（4 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `memory add` | 添加记忆 | `openclaw memory add "重要信息"` |
| `memory search` | 搜索记忆 | `openclaw memory search "Python"` |
| `memory list` | 列出集合 | `openclaw memory list --stats` |
| `memory clear` | 清空记忆 | `openclaw memory clear --collection personal` |

### 监控命令（3 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `stats` | 统计信息 | `openclaw stats --days 7` |
| `top` | TOP 排行榜 | `openclaw top users --limit 10` |
| `benchmark` | 性能测试 | `openclaw benchmark --all-models` |

### 备份命令（3 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `backup` | 创建备份 | `openclaw backup --compress` |
| `restore` | 恢复数据 | `openclaw restore backup.tar.gz` |
| `backup list` | 列出备份 | `openclaw backup list` |

### 安全命令（4 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `user list` | 列出用户 | `openclaw user list` |
| `user grant` | 授予权限 | `openclaw user grant ou_xxx admin` |
| `user revoke` | 撤销权限 | `openclaw user revoke ou_xxx admin` |
| `user audit` | 审计操作 | `openclaw user audit ou_xxx` |

### 插件命令（4 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `plugin list` | 列出插件 | `openclaw plugin list` |
| `plugin install` | 安装插件 | `openclaw plugin install @openclaw/channel-wecom` |
| `plugin update` | 更新插件 | `openclaw plugin update` |
| `plugin uninstall` | 卸载插件 | `openclaw plugin uninstall @openclaw/channel-wecom` |

### 维护命令（3 个）

| 命令 | 说明 | 示例 |
|------|------|------|
| `cleanup` | 清理文件 | `openclaw cleanup --logs --keep-days 7` |
| `optimize` | 优化性能 | `openclaw optimize --memory` |
| `migrate` | 数据迁移 | `openclaw migrate` |

---

## 附录 B：环境变量参考

| 变量名 | 说明 | 默认值 | 示例 |
|--------|------|--------|------|
| `OPENCLAW_PORT` | 网关端口 | 18789 | `export OPENCLAW_PORT=19001` |
| `OPENCLAW_CONFIG` | 配置文件路径 | `~/.openclaw/openclaw.json` | `export OPENCLAW_CONFIG=/etc/openclaw/config.json` |
| `OPENCLAW_WORKSPACE` | 工作空间路径 | `~/.openclaw` | `export OPENCLAW_WORKSPACE=/opt/openclaw` |
| `OPENCLAW_LOG_LEVEL` | 日志级别 | `info` | `export OPENCLAW_LOG_LEVEL=debug` |
| `OPENCLAW_DEV` | 开发模式 | `false` | `export OPENCLAW_DEV=true` |
| `DASHSCOPE_API_KEY` | 通义千问 API Key | - | `export DASHSCOPE_API_KEY=sk-xxx` |
| `QIANFAN_ACCESS_KEY` | 文心一言 Access Key | - | `export QIANFAN_ACCESS_KEY=xxx` |
| `QIANFAN_SECRET_KEY` | 文心一言 Secret Key | - | `export QIANFAN_SECRET_KEY=xxx` |

---

## 附录 C：配置文件完整参考

```json
{
  "version": "1.0",
  "gateway": {
    "port": 18789,
    "host": "0.0.0.0",
    "cors": true,
    "rate_limit": 100
  },
  "channels": {
    "feishu": {
      "enabled": true,
      "appId": "cli_xxx",
      "appSecret": "xxx",
      "encryptKey": "xxx",
      "verificationToken": "xxx"
    },
    "telegram": {
      "enabled": true,
      "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11"
    }
  },
  "models": {
    "default": "qwen-max",
    "providers": {
      "dashscope": {
        "apiKey": "sk-xxx",
        "models": ["qwen-max", "qwen-plus"]
      },
      "qianfan": {
        "accessKey": "xxx",
        "secretKey": "xxx",
        "models": ["ernie-4.0", "ernie-3.5"]
      }
    }
  },
  "agents": {
    "default": "coding-agent",
    "agents": {
      "coding-agent": {
        "model": "qwen-max",
        "systemPrompt": "你是一个专业的编程助手",
        "tools": ["code-interpreter", "file-reader"]
      }
    }
  },
  "tools": {
    "profile": "full",
    "allowed": ["code-interpreter", "file-reader", "web-search"],
    "blocked": ["shell-exec"]
  },
  "memory": {
    "enabled": true,
    "collection": "default",
    "maxItems": 1000
  },
  "security": {
    "dm_policy": "allow",
    "tcc": {
      "enabled": true,
      "maxToolsPerMessage": 5
    }
  }
}
```

---

**文档结束**

---

## 📚 相关文档

- **完整教程**: [openclaw.md](https://github.com/hjs2015/ai-coder/blob/main/docs/openclaw.md)
- **官方文档**: https://docs.openclaw.ai/zh-CN
- **GitHub**: https://github.com/hjs2015/ai-coder

---

**最后更新**: 2026-03-24  
**维护者**: hjs2015
