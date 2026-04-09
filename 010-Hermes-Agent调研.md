# Hermes Agent 调研文档

## 项目概述

Hermes Agent 是由 [Nous Research](https://github.com/nousresearch) 开发的开源自主 AI 智能体框架，于 2026 年 2 月正式发布。项目目前已获得 **28.4k+ Stars**，采用 MIT 许可证开源。

**GitHub 地址**: https://github.com/NousResearch/hermes-agent

**核心定位**: "The agent that grows with you" —— 与你共同成长的 AI Agent

---

## 核心特性

### 1. 自我学习闭环（Built-in Learning Loop）

这是 Hermes Agent 与其他 AI Agent 框架最大的差异点。

#### 自动创建技能（Skill）

- 当 Agent 完成复杂任务（涉及 5+ 工具调用）后，自动从经验中提取模式，生成可复用的技能
- 非平凡工作流检测时主动创建技能
- 用户纠正或错误恢复后触发技能创建

#### 技能自我改进

- 创建出的技能不是一成不变的
- 后续调用时根据执行效果持续优化
- 支持 patch、edit 等操作修改技能内容

#### 记忆持久化

- **双文件架构**：`MEMORY.md` + `USER.md`
- 存储位置：`~/.hermes/memories/`
- 定期提醒保存重要信息
- 跨会话搜索历史对话
- LLM 总结关键内容

#### 用户建模

- 使用 [Honcho](https://github.com/nousresearch/honcho) 对话式建模
- 理解用户偏好、习惯、需求
- 构建个性化用户模型

---

### 2. 跨平台支持

一个 Agent，多个入口：

| 平台 | 说明 |
|------|------|
| **CLI** | 完整 TUI 界面，多行编辑、斜杠命令自动补全、会话历史、中断重定向、流式工具输出 |
| **Telegram** | 语音转文字，跨平台对话 |
| **Discord** | 社区集成 |
| **Slack** | 企业协作集成 |
| **WhatsApp** | 即时通讯集成 |
| **Signal** | 隐私通讯集成 |
| **Email** | 邮件集成 |

只需运行一个 gateway 进程，即可从任何平台访问。

---

### 3. 多模型支持

不绑定任何模型提供商：

| 提供商 | 说明 |
|--------|------|
| Nous Portal | Nous Research 自有服务 |
| OpenRouter | 200+ 模型 |
| z.ai / GLM | 智谱 AI |
| Kimi / Moonshot | 月之暗面 |
| MiniMax | 稀宇科技 |
| OpenAI | GPT 系列 |
| Anthropic | Claude 系列 |
| 自定义端点 | 支持任意 API 兼容服务 |

切换模型命令：`hermes model`

---

### 4. 灵活部署

支持多种部署方式：

| 部署方式 | 适用场景 |
|----------|----------|
| **本地** | 直接在笔记本运行 |
| **Docker** | 容器化部署 |
| **SSH** | 远程服务器 |
| **Daytona** | 无服务器持久化 |
| **Singularity** | 无服务器部署 |
| **Modal** | 空闲时近乎零成本 |

最低配置：可在 **$5 VPS** 上运行，也可扩展至 GPU 集群。

---

## 技术架构

### 记忆系统架构

```
~/.hermes/memories/
├── MEMORY.md      # Agent 通用记忆
└── USER.md        # 用户个性化信息
```

Agent 定期将重要信息总结后写入这些文件，下次会话时可检索使用。

### 技能系统

技能（Skill）是 Hermes Agent 的核心抽象：

- **来源**：从复杂任务经验中自动提取
- **存储**：本地文件系统
- **优化**：使用过程中持续改进
- **调用**：通过自然语言描述需求，Agent 自动匹配相关技能

---

## 快速开始

### 安装

```bash
# 克隆仓库
git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent

# 安装依赖
pip install -r requirements.txt

# 或使用 uv
uv sync
```

### 配置

```bash
# 初始化配置
hermes init

# 设置 API 密钥
hermes config set OPENAI_API_KEY your-key
# 或
hermes config set ANTHROPIC_API_KEY your-key
```

### 运行

```bash
# 启动 CLI
hermes run

# 指定模型
hermes model --provider openrouter --model claude-3.5-sonnet
```

---

## 应用场景

### 1. 个人 AI 助手

- 跨平台统一对话体验
- 越用越懂你的偏好
- 本地部署保护隐私

### 2. 开发助手

- 自动创建复用技能
- 代码编写、调试、重构
- 技术问题解答

### 3. 企业集成

- 钉钉/飞书/企业微信（通过 webhook）
- 客服自动化
- 知识库问答

### 4. 研究工具

- Batch trajectory generation
- Atropos RL 框架集成
- 轨迹收集与评估

---

## 与 OpenClaw 对比

| 特性 | Hermes Agent | OpenClaw |
|------|-------------|----------|
| 学习闭环 | ✅ 内置 | ❌ |
| 技能自动创建 | ✅ 支持 | ❌ |
| 记忆持久化 | ✅ 双文件架构 | ❌ |
| 多平台 | ✅ Telegram/Discord 等 | ✅ |
| 多模型 | ✅ 开放 | ⚠️ 主要 Claude |
| 部署方式 | 多种 | 主要云服务 |

---

## 优缺点分析

### 优点

1. **真正的自学习能力**：不是简单的"记住"，而是持续进化
2. **完全开源**：MIT 协议，可自由使用和修改
3. **隐私友好**：可完全本地部署，数据不上云
4. **多模型支持**：不锁定提供商
5. **跨平台统一**：一个 Agent 多入口

### 缺点

1. **学习曲线**：技能系统需要时间理解
2. **资源需求**：完整功能需要一定硬件配置
3. **配置复杂**：多平台集成需要较多配置工作
4. **社区生态**：相比 Claude Code 生态较新

---

## 总结

Hermes Agent 代表了 AI Agent 的一个新方向 —— 从"工具"到"伙伴"的转变。其内置的学习闭环机制让 Agent 能够真正从经验中成长，而不仅仅是执行命令。这与 OpenClaw 的多 Agent 协作理念形成互补，可以作为个人 AI 助手的另一个选择。

**推荐场景**：注重隐私、需要跨平台使用、期望 AI 能持续学习和进化的用户。

---

## 参考链接

- GitHub: https://github.com/NousResearch/hermes-agent
- Nous Research: https://github.com/nousresearch
- Honcho: https://github.com/nousresearch/honcho
