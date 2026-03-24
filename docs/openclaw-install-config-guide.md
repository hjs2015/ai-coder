# 🦞 OpenClaw 安装配置与命令行使用完全指南

> **来源**：豆包 AI 教程  
> **原文**：https://www.doubao.com/thread/wd131db111f9acf8f  
> **整理时间**：2026-03-24  
> **适用版本**：OpenClaw 2026.3.13+

---

## 📋 目录

1. [systemd 服务配置](#systemd-服务配置)
2. [日志管理](#日志管理)
3. [命令行对话](#命令行对话)
4. [常见问题排查](#常见问题排查)

---

## 🔧 systemd 服务配置

### 问题背景

安装 OpenClaw 后运行以下命令报错：

```bash
root@openclaw:~# systemctl status openclaw
Unit openclaw.service could not be found.

root@openclaw:~# systemctl enable openclaw
Failed to enable unit: Unit file openclaw.service does not exist.
```

**原因分析**：OpenClaw 没有自动注册为 systemd 系统服务。虽然运行了初始化向导，但可能没有选择安装后台守护进程（daemon），或者安装过程没有成功生成服务文件。

---

### 方案一：使用 OpenClaw 自带命令安装

OpenClaw 提供了专门的命令来安装和管理后台服务：

#### 1. 安装守护进程服务

```bash
openclaw daemon install
```

执行成功后，会提示服务文件已创建。

#### 2. 重新加载 systemd 配置

```bash
systemctl daemon-reload
```

#### 3. 启动 OpenClaw 服务

```bash
systemctl start openclaw
```

#### 4. 设置开机自启

```bash
systemctl enable openclaw
```

#### 5. 验证服务状态

```bash
systemctl status openclaw
```

正常情况下，你会看到 `Active: active (running)` 的绿色提示。

---

### 方案二：手动创建 systemd 服务文件

如果 `openclaw daemon install` 命令不可用或报错（如 `systemctl --user unavailable`），可以手动创建系统级服务。

#### 1. 确认 openclaw 的绝对路径

```bash
which openclaw
```

输出示例：
```
/usr/bin/openclaw
```

记下输出的路径，后续配置需要用到。

#### 2. 创建服务文件

```bash
nano /etc/systemd/system/openclaw.service
```

#### 3. 粘贴以下内容

```ini
[Unit]
Description=OpenClaw AI Assistant Gateway
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/.openclaw
ExecStart=/usr/bin/openclaw gateway
Restart=always
RestartSec=5
Environment="HOME=/root"

[Install]
WantedBy=multi-user.target
```

> **注意**：如果 `which openclaw` 查到的路径不是 `/usr/bin/openclaw`，请修改 `ExecStart` 中的路径。

#### 4. 保存并退出

按 `Ctrl+O` 保存，然后按 `Ctrl+X` 退出编辑器。

#### 5. 启动服务并验证

```bash
# 1. 重载 systemd 配置
systemctl daemon-reload

# 2. 启动 OpenClaw 服务
systemctl start openclaw

# 3. 设置开机自启
systemctl enable openclaw

# 4. 查看状态，确认是否运行成功
systemctl status openclaw
```

如果看到绿色的 `Active: active (running)`，说明服务已成功启动。

---

### 备选方案：直接后台运行

如果不想配置 systemd，可以直接在后台运行 gateway：

```bash
# 后台运行 gateway，并将日志输出到 openclaw.log
nohup openclaw gateway > /root/.openclaw/openclaw.log 2>&1 &
```

查看日志确认运行状态：

```bash
tail -f /root/.openclaw/openclaw.log
```

---

## 📝 日志管理

systemd 默认将日志输出到 journald（系统日志守护进程）中，而不是直接写入文件。你有两种选择：

### 方案一：直接查看 journald 日志（推荐）

这是最简单的方法，直接用 systemd 自带的命令查看日志：

#### 实时查看日志

```bash
journalctl -u openclaw -f
```

按 `Ctrl+C` 退出查看。

#### 查看最近 50 条日志

```bash
journalctl -u openclaw -n 50 --no-pager
```

#### 查看今天的日志

```bash
journalctl -u openclaw --since today --no-pager
```

---

### 方案二：修改服务配置，强制输出到指定文件

如果你一定要一个独立的 `.log` 文件，需要修改 `openclaw.service` 文件。

#### 1. 编辑服务文件

```bash
nano /etc/systemd/system/openclaw.service
```

#### 2. 替换为以下内容（新增了日志配置）

```ini
[Unit]
Description=OpenClaw AI Assistant Gateway
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/.openclaw

# 核心修改：将标准输出和错误都重定向到文件
StandardOutput=append:/root/.openclaw/openclaw.log
StandardError=append:/root/.openclaw/openclaw.log

ExecStart=/usr/bin/openclaw gateway
Restart=always
RestartSec=5
Environment="HOME=/root"

[Install]
WantedBy=multi-user.target
```

#### 3. 创建日志文件（防止权限报错）

```bash
touch /root/.openclaw/openclaw.log
```

#### 4. 重载配置并重启服务

```bash
systemctl daemon-reload
systemctl restart openclaw
```

#### 5. 验证日志文件

```bash
# 实时查看
tail -f /root/.openclaw/openclaw.log

# 查看全部
cat /root/.openclaw/openclaw.log
```

---

### 总结

- **图省事**：直接用 `journalctl -u openclaw -f` 看日志
- **必须要文件**：按方案二修改服务配置

---

## 💬 命令行对话

### 前提条件

先确保 OpenClaw 核心网关服务正常运行：

```bash
systemctl status openclaw
```

若显示 `Active: active (running)` 即可正常使用；若未启动，先执行 `systemctl start openclaw` 启动服务。

---

### 方式一：使用终端 UI（推荐）

这是最接近"聊天"的方式，会打开一个基于终端的图形界面：

```bash
openclaw tui
```

进入界面后，你可以像在网页上一样直接打字聊天。

---

### 方式二：使用 agent 命令（单次/脚本对话）

#### 1. 基础单次对话

```bash
openclaw agent --message "你好，介绍一下你自己"
```

#### 2. 交互式连续对话

```bash
openclaw agent --message "你好" --interactive
```

> **注**：如果 `--interactive` 报错，就直接使用方式一的 `tui`。

---

### 方式三：使用 message 命令（通过聊天通道发送）

如果你配置了 Telegram/飞书等通道，可以用这个命令给指定目标发消息：

```bash
# 格式示例（需先配置好 channel）
openclaw message send --channel feishu --target "你的飞书名字" --message "在吗"
```

---

### 进阶用法（自定义对话参数）

#### 1. 指定对话使用的模型

```bash
# 单次对话指定模型
openclaw agent --model modelstudio/qwen3.5-plus --message "用 Python 写一个端口扫描脚本"

# 交互式会话指定模型
openclaw agent -i --model modelstudio/glm-4.7
```

查看已配置的所有可用模型：

```bash
openclaw models list
```

#### 2. 设定系统提示词（固定 AI 角色）

```bash
# 示例：设定为运维专家角色
openclaw agent --system-prompt "你是资深 Linux 运维专家，回答只给可直接执行的命令，不写废话" --message "查看服务器当前内存占用 TOP10 的进程"
```

#### 3. 调整模型输出参数

```bash
# 调整温度值（0=最严谨确定，1=最随机发散，默认 0.7）
openclaw agent --temperature 0.2 --message "写一份企业级服务器安全规范"
```

---

### 交互式会话内常用快捷命令

在 `openclaw tui` 交互式对话中，可直接输入以下斜杠命令控制会话：

| 命令 | 核心作用 |
|------|---------|
| `/new` 或 `/reset` | 清空当前会话上下文，开启全新对话，避免 Token 累积消耗 |
| `/model 模型名` | 实时切换当前会话使用的 AI 模型 |
| `/status` | 查看当前会话的模型信息、Token 用量、费用估算 |
| `/compact` | 自动压缩对话上下文，保留核心要点，大幅减少 Token 消耗 |
| `/help` | 查看完整的斜杠命令列表 |
| `/exit` | 退出交互式对话模式 |

---

## 🔍 常见问题排查

### 问题 1：执行命令无响应/报错

先执行以下命令查看网关实时日志：

```bash
journalctl -u openclaw -f
```

排查模型 API 是否连通、API Key 是否有效。

---

### 问题 2：提示 `No model configured`

说明模型配置缺失，执行以下命令重新配置模型和 API Key：

```bash
openclaw configure --section model
```

---

### 问题 3：多轮对话上下文丢失

确保每次对话都在同一个 `openclaw tui` 交互式会话内执行，单次对话模式不会保留上下文。

---

### 问题 4：命令拼写错误

常见错误：

```bash
# ❌ 错误
openclaw gatewat status

# ✅ 正确
openclaw gateway status
```

---

### 问题 5：unknown command 'chat'

在 OpenClaw 2026.3.13 版本中，没有 `chat` 命令，正确的对话命令是：

```bash
# ✅ 使用 tui（终端界面）
openclaw tui

# ✅ 使用 agent（命令行）
openclaw agent --message "你好"

# ✅ 使用 agent 交互模式
openclaw agent --message "你好" --interactive
```

查看完整帮助：

```bash
openclaw --help
```

---

## 📊 常用管理命令速查

```bash
# 查看服务状态
systemctl status openclaw

# 启动服务
systemctl start openclaw

# 停止服务
systemctl stop openclaw

# 重启服务
systemctl restart openclaw

# 查看服务日志
journalctl -u openclaw -f

# 查看最近 50 条日志
journalctl -u openclaw -n 50 --no-pager

# 查看今天的日志
journalctl -u openclaw --since today --no-pager

# 查看 openclaw 版本
openclaw -v

# 查看帮助
openclaw --help

# 打开 Dashboard
openclaw dashboard

# 终端 UI 对话
openclaw tui

# 命令行对话
openclaw agent --message "你好"

# 列出可用模型
openclaw models list

# 配置模型
openclaw configure --section model
```

---

## 📚 参考链接

- **OpenClaw 官方文档**：https://docs.openclaw.ai/
- **GitHub**：https://github.com/openclaw/openclaw
- **豆包原文**：https://www.doubao.com/thread/wd131db111f9acf8f

---

## 📝 文档说明

**本文档基于豆包 AI 教程整理**，内容经过系统化编排，便于查阅和学习。

**最后更新**：2026-03-24  
**适用版本**：OpenClaw 2026.3.13+
