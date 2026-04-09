它会对标 OpenClaw，但做法完全不一样

今天聊个有意思的项目——Hermes Agent，来自 AI 研究团队 Nous Research。

如果你对 AI Agent 有了解，大概率知道 OpenClaw。Hermes 做的事和它很像，但切入角度有一个本质区别：**它真的会自己进步**。

不是营销话术，是产品层面真的这么设计的。
![image.png](https://pic.itzhouq.cn/20260409142719236.png)

## 简单说它能做什么

**自改进学习循环**

这是 Hermes 最核心的能力。它会从对话中提取经验，主动创建 Skills，在使用过程中自动优化这些 Skills，还会搜索历史对话来回顾上下文。简单讲：它不只是回答你的问题，它在回答过程中学习怎么下次答得更好。

**多模型随意切换**

OpenRouter 上 200+ 模型随便选，Kimi、MiniMax、GLM、OpenAI 等，一句命令切换，不用改代码。适合想对比不同模型效果的用户。

**多平台覆盖**

飞书、Telegram、Discord、Slack、WhatsApp、Signal、Email、CLI，手机电脑都能接。一个 gateway 进程管理所有平台。

**几乎零成本运行**

支持 Daytona 和 Modal 的 serverless 模式——不用的时候环境休眠，完全不花钱；消息一来立刻唤醒。官方说 $5 的 VPS 就能跑。

**OpenClaw 迁移支持**

自带迁移脚本 `hermes claw migrate`，配置、记忆、Skills、API Keys 全部迁移。也可以先跑 `--dry-run` 预览内容。

**40+ 工具 + Cron + 子 Agent + MCP 扩展**，支持批量轨迹生成等研究场景。

## 和 OpenClaw 相比怎么样

说实话，两个产品定位非常接近，都在做"AI Agent 平台"，支持多模型、多平台、Skills 系统。

核心差异在于：

| 维度        | Hermes Agent | OpenClaw    |
| --------- | ------------ | ----------- |
| 自改进能力     | ✅ 内置学习循环     | ❌ 无此设计      |
| 飞书集成      | ✅ 原生支持       | ✅ 原生支持      |
| GitHub 集成 | ❌            | ✅ 原生支持      |
| 插件生态      | Skills 系统    | AgentSkills |
| 企业场景      | 偏极客/研究者      | 偏企业/团队      |

OpenClaw 的强项是飞书、GitHub 这类企业场景集成，Hermes 的强项是"越用越懂你"的自改进能力。

如果你已经在用 OpenClaw，迁移收益不大——尤其是你依赖飞书集成的。但如果你是 AI 研究者或极客用户，想体验真正的自改进 Agent，可以试试。

**AI Agent 赛道正在变有意思。** 以前大家比的是"谁接的平台多"，现在开始卷"谁更懂用户"。这场竞争，对用户来说是好消息。

关注公众号后私信" Hermes "获取项目地址和快速上手指南。