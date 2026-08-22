# KnowYourSelf — 面向 AI Agent 的個人知識作業系統

[English](README.md) · [简体中文](README.zh-CN.md) · **繁體中文**

**KnowYourSelf** 是一個開源、廠商中立的 **Personal Knowledge OS（個人知識作業系統）** 框架，用於組織個人知識管理（PKM）、AI Agent Context Engineering，以及 Human-in-the-loop AI 協作。

它適用於：

- 個人生活與長期事務
- 學習與研究
- 多家公司或客戶環境
- SaaS 產品管理與產品探索
- 軟體專案與 GitHub 工程
- ChatGPT、Claude、Codex、Cursor、Gemini 等 AI Agent
- 專案級 AI Context / Project Memory
- Daily Project Reliability Audit
- Personal Compounding / 個人成長複利復盤

> **Local Detail, Global Summary｜細節留在專案，總體只看摘要。**

## 它解決什麼問題？

隨著 AI Coding Agent 和通用 Agent 越來越強，瓶頸正從「程式碼能不能產生」轉向：

- 上下文是否正確；
- 產品決策是否清晰；
- Agent 是否拿到了真正需要的資訊；
- 長期專案狀態能否持續；
- 多個專案之間是否會發生 Context Pollution；
- Human-in-the-loop 的職責邊界是否清楚。

一個常見錯誤是把整個 Repo、幾個月的聊天記錄、全部 Design 文件和所有知識筆記一起塞給 Agent。

**KnowYourSelf 不採用這種方式。**

它把「系統中存在的知識」和「當前任務真正載入的上下文」分開，讓 Agent 按照 Security Domain → Project → Feature → Task → Evidence 漸進式取得資訊。

## 核心架構

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

使用 Notion、飛書或其他協作文檔系統，負責日常編輯、專案工作台、決策、學習、研究、Review 和長期知識。

### Engineering Truth Layer

使用 GitHub + Git + Markdown / JSON / YAML 保存程式碼、測試、技術 Contract、版本化決策和工程事實。

### Agent Context Layer

使用 Context Projection 向 AI Agent 提供 Task-scoped Context，避免遞迴載入整個知識庫。

### Portfolio Control Layer

使用 Project Health Snapshot 做跨專案健康度、風險、待 Owner 決策、待 Owner 驗收以及重複 Failure 的總體治理。

## 六條核心原則

### 1. Local Detail, Global Summary

**專案維護細節，總體只看摘要。**

Portfolio 層預設只讀：

- 專案狀態
- 待 Owner 決策
- 待 Owner 驗收
- 當前風險
- 重複 Failure Pattern
- 下一步

不會遞迴讀取所有專案正文。

### 2. No Recursive Context Boot

不要這樣啟動 Agent：

```text
Knowledge OS Root
→ 所有公司
→ 所有專案
→ 所有文件
→ 所有歷史
→ 當前任務
```

而應該：

```text
Global Minimal
→ Security Domain
→ Project
→ Feature
→ Task
→ Relevant Evidence
```

### 3. Knowledge Available ≠ Context Loaded

一份文件可以：

```text
AVAILABLE
SEARCHABLE
READABLE
LOADED
WRITABLE
```

其中「可搜尋」不等於「每次都進入模型上下文」。預設採用最小化載入與 Just-in-time Retrieval。

### 4. Conversation is Ephemeral; State is Persistent

聊天是臨時思考空間，專案狀態必須落到持久化 Artifact。

長 Session 應在階段邊界建立 `SESSION_HANDOVER.md`，保存：

- 當前目標
- 已接受決定
- 當前實作狀態
- 重要證據
- OPEN 問題
- 下一步

新的 Session 優先讀取 Handover，而不是恢復整個聊天歷史。

### 5. Security Domain First

檢索順序：

```text
Security Domain → Project → Feature → Task → Topic
```

跨公司、跨安全域訪問預設拒絕。

### 6. One Fact, One Source of Truth

推薦：

| 資訊類型 | 權威位置 |
| --- | --- |
| Human 探索 | Human Workspace |
| 凍結產品決策 | Decision Log / Product Contract |
| 工程實作 | GitHub |
| 當前任務 | Task Packet |
| 實作證據 | Review Pack |
| 重複協作失效 | Failure Registry |

禁止同一份正式事實在 Notion、Obsidian、Git、聊天之間無控制地雙向維護。

## Human-in-the-loop 模型

### Owner / Human

負責：

- Intent
- 產品判斷
- Priority
- 視覺方向
- Security Boundary
- Scope Freeze
- 最終驗收
- Release / Merge

### Main Agent

負責：

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

負責：

- 有邊界的實作
- 測試
- Contained Self-repair
- Evidence
- Draft PR

執行 Agent 不應自行修改已凍結產品決定、跨安全域、擴大 Scope 或自動 Merge。

## GPT 和 Codex 怎麼分工？

推薦：

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

通用推理模型更適合 Discovery、架構設計、知識設計、產品決策和持續訪談；Codex 等 Coding Agent 更適合在 Scope 凍結後執行具體工程任務。

## Project Capsule 與 Feature Capsule

大型專案不應讓 Agent「進入專案就讀取全部」。

推薦：

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

`PROJECT_ENTRY.md` 是地圖，不是百科全書。

當前只處理 Feature A，就載入 Feature A 的 Context，而不是整個 Project。

## Project Health Snapshot

每個活躍專案可以輸出一份很薄的健康摘要，包括：

- GREEN / YELLOW / RED
- 今日關鍵變更
- 待我決策
- 待我驗收
- 風險
- Active PR
- 新回歸與 Baseline Failure
- Context Health
- 重複 Failure Pattern
- 下一步

Portfolio 層使用這些摘要進行每日專案可靠性檢查和每週 Portfolio Review。

## 兩套持續改進機制

### Project Reliability Loop

```text
Project Activity
→ Daily Collaboration Audit
→ Failure Registry
→ Rule Promotion
→ Rule Retirement
```

重點檢查：

- Scope Drift
- 過大的變更
- Git Base / Head 錯誤
- Stale Context
- Design Drift
- Visual Validation 太晚
- Harness / CI 過重
- Agent 權限問題
- PR / Workflow 重複失敗

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

AI 不應只問「今天什麼最有價值」，而應先從真實行為證據中提出價值候選，再追問少量高價值問題。

目標是讓工作轉化為：

**認知 → 知識 → 技能 → 判斷力**

而不是多出另一份沒人想看的日報。

## 常見使用場景

### Personal Knowledge Management / PKM

建立長期個人知識系統，同時避免把所有筆記、專案、附件和程式碼放進一個巨型 Context。

### Personal AI Operating System

管理個人知識、專案、學習、Review、AI Memory 和長期工作流。

### Multi-project AI Agent Management

同時管理多個 AI 專案，讓每個專案擁有自己的 Context，同時讓 Portfolio 只查看健康摘要。

### Multi-company Knowledge Management

不同公司使用獨立 Security Domain；個人入口可以統一，但資料訪問不能混在一起。

### Human-in-the-loop Product Development

Human 負責 Intent、判斷和驗收，AI 負責 Context Compilation、Planning、Execution Handoff 和 Evidence Review。

### AI Coding Agent Workflow

將 Product Requirement、Design、Task Packet、GitHub、Tests、Review Evidence 和 Session Handover 連接起來，同時避免把整個 Repo 塞進 Prompt。

### Context Engineering for AI Agents

透過 Progressive Disclosure、Task-scoped Retrieval、Project Capsule、Feature Capsule 和 Session Handover 管理 Agent Context。

### AI Agent Memory / Persistent State

區分 Stable Memory、Project Memory 和 Session Memory，避免 Agent 長期累積無關上下文。

## 5 分鐘開始

### 第一步：把 Bootstrap Prompt 給一個通用推理 Agent

開啟 [`prompts/BOOTSTRAP_AGENT.md`](prompts/BOOTSTRAP_AGENT.md)，發送給 GPT、Claude、Gemini 或其他強推理模型。

然後告訴它：

> 請完整閱讀這個 Prompt。現在只進入 DISCOVERY，不建立 Notion 頁面、資料庫、自動化，也不要遷移任何資料。嚴格遵守 Local Detail, Global Summary 和 No Recursive Context Boot。每輪只問我一個最高價值的問題。

第一階段是「持續問答」，不是搬家。

### 第二步：凍結架構後再實施

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

第一輪只搭：

- Personal HQ
- 一個個人專案
- 一個知識主題
- 一個 Company Pointer
- 一個 Project Capsule
- 一個 Feature Capsule
- 一個 Project Health Snapshot
- 一個 Session Handover
- 一個 Context Projection 範例

不要第一天搬遷全部歷史資料。

## 建議工具分工

```text
Notion / 飛書
= Human 編輯與協作知識層

Google Drive
= PDF、資料集、影片、大型檔案與備份

GitHub
= 工程事實、Contracts 與程式碼

Obsidian（可選）
= 個人 Markdown 研究庫 / 離線歸檔
```

工具不重要，規則更重要：**一個正式事實只應有一個權威來源；Agent Context 必須有清晰邊界。**

## FAQ

### KnowYourSelf 是 Notion 模板嗎？

不是。它是知識架構與 AI Agent 協作框架。Notion、飛書、Google Drive、GitHub、Obsidian 或其他工具都可以實作其中不同層。

### 它只是 Prompt Engineering 嗎？

不是。Prompt 只是一小層。核心是 Context Engineering、State Management、Project Memory、Security Domain、Project Capsule、Session Handover、Evaluation、Human Review 與持續改進。

### Agent 會讀取我的整個知識庫嗎？

不會。目標架構採用 Task-scoped Context Projection，按 Security Domain、Project、Feature 和 Task 按需讀取。

### 可以使用 Codex 嗎？

可以。Codex 可以作為 Execution Agent，在主 Agent 編譯出凍結 Scope 和 Implementation Packet 後負責工程執行。

### 可以管理多家公司嗎？

可以，但每家公司必須作為獨立 Security Domain。統一 Dashboard 不等於統一資料訪問。

### 這個系統只能用於軟體開發嗎？

不是。它同樣可以管理個人知識、研究、學習、產品工作、專案和長期任務。工程只是額外增加 Git 事實層。

### Local Detail, Global Summary 解決什麼問題？

它解決多專案 Context Explosion。專案細節留在專案內部，Portfolio 只消費結構化摘要。

### Session Handover 是什麼？

一份緊湊的持久狀態文件，讓新的 AI Session 不需要重播全部歷史對話就可以繼續工作。

## 文件

- [`Bootstrap Agent Prompt`](prompts/BOOTSTRAP_AGENT.md)
- [`Highest-Level Principles`](principles/HIGHEST_LEVEL_PRINCIPLES.md)
- [`Owner Quick Start`](docs/OWNER_QUICK_START.md)
- [`Interview State Schema`](schemas/interview_state.yaml)
- [`Project Router Schema`](schemas/project_router.json)
- [`Security Policy`](SECURITY.md)
- [`Contributing Guide`](CONTRIBUTING.md)
- [`Changelog`](CHANGELOG.md)

## 語言版本

- [English (default)](README.md)
- [简体中文](README.zh-CN.md)
- **繁體中文**

## 搜索主題

本專案適用於搜尋與研究：**個人知識管理（PKM）、Personal AI Operating System、AI Knowledge Base、AI Agent Memory、Persistent AI Memory、Agent Context Management、Context Engineering、Context Window Management、Human-in-the-loop AI、多 Agent 工作流、AI Coding Agent、Codex Workflow、Claude Code、Project Context、Project Memory、Session Handover、AI Agent Orchestration、Notion 知識管理、Obsidian 知識管理、GitHub AI Workflow、Prompt Engineering、Agent Reliability、AI Workflow Automation、Project Health Monitoring、Failure Registry、Knowledge Governance、Portable AI Memory、多公司知識管理**。

## License

MIT. See [`LICENSE`](LICENSE)。
