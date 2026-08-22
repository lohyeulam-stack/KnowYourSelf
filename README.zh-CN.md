# KnowYourSelf — 面向 AI Agent 的个人知识操作系统

[English](README.md) · **简体中文** · [繁體中文](README.zh-TW.md)

**KnowYourSelf** 是一个开源、厂商无关的 **Personal Knowledge OS（个人知识操作系统）** 框架，用于组织个人知识管理（PKM）、AI Agent 上下文工程（Context Engineering）和 Human-in-the-loop AI 协作。

它适用于：

- 个人生活与长期事务
- 学习与研究
- 多家公司或客户环境
- SaaS 产品管理与产品探索
- 软件项目与 GitHub 工程
- ChatGPT、Claude、Codex、Cursor、Gemini 等 AI Agent
- 项目级 AI Context / Project Memory
- Daily Project Reliability Audit
- Personal Compounding / 学习复利复盘

> **Local Detail, Global Summary｜细节留在项目，总体只看摘要。**

## 它解决什么问题？

随着 AI 编程 Agent 和通用 Agent 越来越强，瓶颈正在从“代码能不能生成”转向：

- 上下文是否正确；
- 产品决策是否清晰；
- Agent 是否拿到了真正需要的信息；
- 长期项目状态能否持续；
- 多项目之间是否会发生上下文污染；
- Human-in-the-loop 的职责边界是否明确。

一个常见错误是把整个代码仓库、几个月的聊天记录、所有设计文档和所有知识笔记一起塞给 Agent。

**KnowYourSelf 不采用这种方式。**

它将知识分为“可存在”和“真正加载进入当前任务上下文”两个层次，让 Agent 按 Security Domain → Project → Feature → Task → Evidence 渐进式获取上下文。

## 核心架构

```text
Global Minimal Rules
        ↓
Security Domain
        ↓
Project Capsule
        ↓
Feature Capsule
        ↓
Current Task
        ↓
Relevant Evidence
```

### Human Knowledge Layer

使用 Notion、飞书或其他协作型文档系统，负责日常编辑、项目工作台、决策、学习、研究、Review 和长期知识。

### Engineering Truth Layer

使用 GitHub + Git + Markdown / JSON / YAML 保存代码、测试、技术合同、版本化决定和工程事实。

### Agent Context Layer

使用 Context Projection 向 AI Agent 提供任务级上下文，避免递归加载整个知识库。

### Portfolio Control Layer

使用 Project Health Snapshot 做跨项目健康度、风险、待我决定、待我验收以及重复 Failure 的总体检查。

## 六条核心原则

### 1. Local Detail, Global Summary

**项目维护细节，总体只看摘要。**

Portfolio 层默认只读取：

- 项目状态
- 待 Owner 决定
- 待 Owner 验收
- 当前风险
- 重复 Failure Pattern
- 下一步

不会递归读取所有项目正文。

### 2. No Recursive Context Boot

不要这样启动 Agent：

```text
Knowledge OS 根目录
→ 所有公司
→ 所有项目
→ 所有文档
→ 所有历史
→ 当前任务
```

而应该：

```text
Global Minimal
→ Security Domain
→ Project
→ Feature
→ Task
→ Relevant Evidence
```

### 3. Knowledge Available ≠ Context Loaded

文档可以：

```text
AVAILABLE
SEARCHABLE
READABLE
LOADED
WRITABLE
```

其中“可搜索”不等于“每次都进入模型上下文”。默认采用最小化加载和 Just-in-time Retrieval。

### 4. Conversation is Ephemeral; State is Persistent

聊天是临时思考空间，项目状态必须落到持久化 Artifact。

长会话应在阶段边界生成 `SESSION_HANDOVER.md`，保存：

- 当前目标
- 已接受决定
- 当前实现状态
- 重要证据
- OPEN 问题
- 下一步

新 Session 优先读取 Handover，而不是恢复整个聊天历史。

### 5. Security Domain First

检索顺序：

```text
Security Domain → Project → Feature → Task → Topic
```

跨公司、跨安全域访问默认拒绝。

### 6. One Fact, One Source of Truth

推荐事实来源：

| 信息类型 | 权威位置 |
| --- | --- |
| Human 探索 | Human Workspace |
| 冻结产品决定 | Decision Log / Product Contract |
| 工程实现 | GitHub |
| 当前任务 | Task Packet |
| 实现证据 | Review Pack |
| 重复协作失效 | Failure Registry |

禁止同一正式事实在 Notion、Obsidian、Git、聊天之间无控制地双向维护。

## Human-in-the-loop 模型

### Owner / Human

负责：

- Intent
- 产品判断
- Priority
- 视觉方向
- Security Boundary
- Scope Freeze
- 最终验收
- Release / Merge

### Main Agent

负责：

- Discovery
- Context Routing
- Task Classification
- Contract Compilation
- Project Memory
- Execution Handoff
- Evidence Review
- Audit
- Coaching

### Execution Agent

例如 Codex、Claude Code、Cursor Agent。

负责：

- 有边界的实现
- 测试
- Contained Self-repair
- Evidence
- Draft PR

执行 Agent 不应自行修改已经冻结的产品决定、跨安全域、扩大 Scope 或自动 Merge。

## GPT 和 Codex 怎么分工？

推荐：

```text
Human
  ↓
Main Agent / GPT / Claude
  ↓
Discovery
  ↓
Architecture Options
  ↓
Owner Decision
  ↓
Frozen Scope
  ↓
Implementation Packet
  ↓
Codex / Execution Agent
  ↓
Evidence + Review Pack
  ↓
Human Acceptance
```

通用推理模型更适合 Discovery、架构设计、知识设计、产品决策和持续访谈；Codex 等 Coding Agent 更适合在 Scope 冻结后执行具体工程任务。

## Project Capsule 与 Feature Capsule

大型项目不应让 Agent “进入项目就读取全部”。

推荐：

```text
project/
├── PROJECT_ENTRY.md
├── PROJECT_CONTEXT.yaml
├── CURRENT_STATE.md
├── DECISIONS_INDEX.md
├── PROJECT_HEALTH_SNAPSHOT.yaml
├── SESSION_HANDOVER.md
└── features/
    ├── feature-a/
    ├── feature-b/
    └── feature-c/
```

`PROJECT_ENTRY.md` 是地图，不是百科全书。

当前只做 Feature A，就加载 Feature A 的 Context，不加载整个项目。

## Project Health Snapshot

每个活跃项目可以输出一份很薄的健康摘要，包括：

- GREEN / YELLOW / RED
- 今日关键变化
- 待我决定
- 待我验收
- 风险
- Active PR
- 新回归与 Baseline Failure
- Context Health
- 重复 Failure Pattern
- 下一步

Portfolio 层使用这些摘要进行每日项目可靠性检查和每周项目组合复盘。

## 两套持续改进机制

### Project Reliability Loop

```text
Project Activity
→ Daily Collaboration Audit
→ Failure Registry
→ Rule Promotion
→ Rule Retirement
```

重点检查：

- Scope Drift
- 过大的变更
- Git Base / Head 错误
- Stale Context
- Design Drift
- Visual Validation 太晚
- Harness / CI 过重
- Agent 权限问题
- PR / Workflow 重复失败

### Personal Compounding Loop

```text
Evidence
→ Candidate Value
→ Guided Questions
→ Human Confirmation
→ Cognition Delta
→ Knowledge
→ Skill Evidence
→ Deliberate Practice
```

AI 不应该简单问“今天什么最有价值”，而是先从真实行为证据里提取候选，再追问少量高价值问题。

目标是让工作转化为：

**认知 → 知识 → 技能 → 判断力**

而不是产生另一份没人想看的日报。

## 常见使用场景

### Personal Knowledge Management / PKM

建立长期个人知识系统，同时避免把所有笔记、项目、附件和代码放进一个巨型上下文。

### Personal AI Operating System

管理个人知识、项目、学习、Review、AI Memory 和长期工作流。

### Multi-project AI Agent Management

同时管理多个 AI 项目，并让每个项目拥有自己的 Context，同时让 Portfolio 只查看健康摘要。

### Multi-company Knowledge Management

不同公司使用独立 Security Domain；个人入口可以统一，但数据访问不能混在一起。

### Human-in-the-loop Product Development

Human 负责 Intent、判断和验收，AI 负责 Context Compilation、Planning、Execution Handoff 和 Evidence Review。

### AI Coding Agent Workflow

将 Product Requirement、Design、Task Packet、GitHub、Tests、Review Evidence 和 Session Handover 连接起来，同时避免把整个 Repo 塞进 Prompt。

### Context Engineering for AI Agents

通过 Progressive Disclosure、Task-scoped Retrieval、Project Capsule、Feature Capsule 和 Session Handover 管理 Agent Context。

### AI Agent Memory / Persistent State

区分 Stable Memory、Project Memory 和 Session Memory，避免 Agent 长期积累无关上下文。

## 5 分钟开始

### 第一步：把 Bootstrap Prompt 给一个通用推理 Agent

打开 [`prompts/BOOTSTRAP_AGENT.md`](prompts/BOOTSTRAP_AGENT.md)，发送给 GPT、Claude、Gemini 或其他强推理模型。

然后告诉它：

> 请完整阅读这个 Prompt。现在只进入 DISCOVERY，不创建 Notion 页面、数据库、自动化，也不要迁移任何资料。严格遵守 Local Detail, Global Summary 和 No Recursive Context Boot。每轮只问我一个最高价值的问题。

第一阶段是“持续问答”，不是搬家。

### 第二步：冻结架构后再实施

```text
DISCOVERY
→ ARCHITECTURE_OPTIONS
→ DECISION_REVIEW
→ SCOPE_FROZEN
→ PILOT_BUILD
→ PILOT_REVIEW
→ FULL_BUILD
→ MIGRATION
→ GOVERNANCE
```

### 第三步：只做小 Pilot

第一轮只搭：

- Personal HQ
- 一个个人项目
- 一个知识主题
- 一个 Company Pointer
- 一个 Project Capsule
- 一个 Feature Capsule
- 一个 Project Health Snapshot
- 一个 Session Handover
- 一个 Context Projection 示例

不要第一天搬迁全部历史资料。

## 推荐工具分工

```text
Notion / 飞书
= Human 编辑与协作知识层

Google Drive
= PDF、数据集、视频、大文件与备份

GitHub
= 工程事实、合同与代码

Obsidian（可选）
= 个人 Markdown 研究库 / 离线归档
```

工具不重要，规则更重要：**一个正式事实只应有一个权威来源；Agent 上下文必须有边界。**

## FAQ

### KnowYourSelf 是 Notion 模板吗？

不是。它是知识架构与 AI Agent 协作框架。Notion、飞书、Google Drive、GitHub、Obsidian 或其他工具都可以实现其中不同层。

### 它只是 Prompt Engineering 吗？

不是。Prompt 只是很小的一层。核心是 Context Engineering、State Management、Project Memory、Security Domain、Project Capsule、Session Handover、Evaluation、Human Review 和持续改进。

### Agent 会读取我的整个知识库吗？

不会。目标架构采用 Task-scoped Context Projection，按 Security Domain、Project、Feature 和 Task 按需读取。

### 可以使用 Codex 吗？

可以。Codex 可以作为 Execution Agent，在主 Agent 编译出冻结 Scope 和 Implementation Packet 后负责工程执行。

### 可以管理多家公司吗？

可以，但每家公司必须作为独立 Security Domain。统一 Dashboard 不等于统一数据访问。

### 这个系统只能用于软件开发吗？

不是。它同样可以管理个人知识、研究、学习、产品工作、项目和长期任务。工程只是额外增加了 Git 事实层。

### Local Detail, Global Summary 解决什么问题？

它解决多项目 Context Explosion。项目细节留在项目内部，Portfolio 只消费结构化摘要。

### Session Handover 是什么？

一份紧凑的持久状态文件，让新的 AI Session 不需要重放全部历史对话就可以继续工作。

## 文档

- [`Bootstrap Agent Prompt`](prompts/BOOTSTRAP_AGENT.md)
- [`Highest-Level Principles`](principles/HIGHEST_LEVEL_PRINCIPLES.md)
- [`Owner Quick Start`](docs/OWNER_QUICK_START.md)
- [`Interview State Schema`](schemas/interview_state.yaml)
- [`Project Router Schema`](schemas/project_router.json)
- [`Security Policy`](SECURITY.md)
- [`Contributing Guide`](CONTRIBUTING.md)
- [`Changelog`](CHANGELOG.md)

## English / 繁體中文

- [English (default)](README.md)
- **简体中文**
- [繁體中文](README.zh-TW.md)

## 搜索主题

本项目适用于搜索和研究：**个人知识管理（PKM）、个人 AI 操作系统、AI 知识库、AI Agent Memory、AI Agent 上下文管理、Context Engineering、Context Window Management、Human-in-the-loop AI、多 Agent 工作流、AI Coding Agent、Codex 工作流、Claude Code、Project Context、Project Memory、Session Handover、AI Agent Orchestration、Notion 知识管理、Obsidian 知识管理、GitHub AI 工作流、Prompt Engineering、Agent Reliability、AI Workflow Automation、Project Health Monitoring、Failure Registry、Knowledge Governance、Portable AI Memory、多公司知识管理**。

## License

MIT. See [`LICENSE`](LICENSE)。
