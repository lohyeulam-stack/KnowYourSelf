# Owner Quick Start

## Start a new Bootstrap session

Give the agent `prompts/BOOTSTRAP_AGENT.md`, then say:

> 请完整阅读。现在只进入 Discovery，不允许创建页面、数据库、自动化或迁移资料。严格遵守 Local Detail, Global Summary 和 No Recursive Context Boot。每轮只问我一个最高价值问题。

## Check state

`/status`

The agent should return: current stage, confirmed, superseded, open questions, risks and next gate.

## Change a previous answer

> 修改之前关于【主题】的答案。旧答案标记 SUPERSEDED。新答案是：……

## Pause questions and summarize

> 先不要继续提问。总结：已确认 / OPEN / 冲突 / RECOMMENDATION / 下一 Gate。

## Architecture review

> 进入 ARCHITECTURE_OPTIONS。至少给两个结构不同的方案，不实施。

## Freeze

`/freeze 【范围】`

Only explicitly accepted content becomes frozen.

## Build only the Pilot

`/build-pilot`

Implement only frozen Pilot scope. Do not migrate all history.

## Context becomes too large

> 你正在违反 No Recursive Context Boot。停止全文扫描，重新按 Security Domain → Project → Feature → Task 生成最小 Context。

## Multiple projects are loaded

> 违反 Local Detail, Global Summary。项目细节留在项目内，Portfolio 只允许读取 Project Health Snapshot。

## Long session

> 生成 SESSION_HANDOVER。Conversation is Ephemeral; State is Persistent。后续从 Handover 继续。

## Agent starts building too early

> 停止实施。当前 Architecture 尚未 Frozen。回到 Discovery / Review。
