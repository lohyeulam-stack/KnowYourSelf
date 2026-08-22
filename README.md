# KnowYourSelf — Federated Personal Knowledge OS for AI Agents

**KnowYourSelf** is an open-source, vendor-neutral framework for **personal knowledge management (PKM)**, **AI agent context engineering**, and **human-in-the-loop AI workflows** across personal life, learning, multiple companies, product work, software projects, and GitHub-based engineering.

> **Local Detail, Global Summary.**
>
> Keep detailed context inside each project. Let the portfolio layer consume compact project health summaries. Give an AI agent only the context required for the current task.

**Languages:** **English** · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md)

## What is KnowYourSelf?

KnowYourSelf is a practical architecture for people who use **ChatGPT, Claude, Codex, Cursor, Gemini, and other AI coding or reasoning agents** as part of daily work.

It combines:

- personal knowledge management (PKM)
- AI knowledge bases and project memory
- context engineering for AI agents
- human-in-the-loop product development
- multi-agent workflow orchestration
- project and feature context capsules
- session handover and persistent state
- security-domain isolation for multiple companies
- project health monitoring
- failure analysis and continuous workflow improvement

The framework is designed for one recurring problem:

> **How do you give AI agents enough context to do reliable work without loading your entire knowledge base into every task?**

KnowYourSelf is not a giant Markdown dump and not just a prompt engineering library. It is a knowledge architecture for deciding **what exists, what is canonical, what an agent should load, what an agent may change, and how a human reviews the result**.

## Why this architecture exists

As AI-assisted development becomes more capable, the bottleneck increasingly moves from raw code generation to **context quality, decision quality, workflow design, evaluation, and verification**.

A common failure mode is to give an agent an entire repository, a giant `AGENTS.md`, months of chat history, every design document, and every project note. More context does not automatically produce better decisions.

KnowYourSelf uses progressive, task-scoped context:

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

This makes the framework useful for **AI agent memory, context management, multi-project AI workflows, and long-running agent sessions**.

## Core architecture

### Human Knowledge Layer

Use a human-friendly workspace such as **Notion, Feishu, or another collaborative document system** for everyday editing, project workbenches, decisions, notes, research, reviews, and learning.

### Engineering Truth Layer

Use **GitHub + Git + Markdown / JSON / YAML** as the engineering source of truth for code, tests, technical contracts, versioned decisions, and implementation artifacts.

### Agent Context Layer

Use **Context Projection** so AI agents receive task-scoped context instead of recursively loading an entire knowledge base.

### Portfolio Control Layer

Use compact **Project Health Snapshots** for cross-project governance, daily project audits, risk tracking, pending owner decisions, and repeated failure patterns.

## Core principles

### 1. Local Detail, Global Summary

**Project details stay inside projects. Global views consume summaries.**

A portfolio dashboard should normally read:

- project status
- pending owner decisions
- pending owner reviews
- current risks
- repeated failure patterns
- next steps

It should not recursively load every project document by default.

### 2. No Recursive Context Boot

Do not start an AI task like this:

```text
Knowledge OS Root
→ all companies
→ all projects
→ all documents
→ all history
→ current task
```

Instead route context progressively:

```text
Global Minimal
→ Security Domain
→ Project
→ Feature
→ Task
→ Relevant Evidence
```

### 3. Knowledge Available ≠ Context Loaded

A document can be searchable and readable without being injected into every agent prompt.

KnowYourSelf distinguishes:

```text
AVAILABLE
SEARCHABLE
READABLE
LOADED
WRITABLE
```

The default should be minimal loading and just-in-time retrieval.

### 4. Conversation is Ephemeral; State is Persistent

Long AI conversations should not become the only source of project memory.

At meaningful boundaries, create a **Session Handover** containing:

- current goal
- accepted decisions
- current implementation state
- important evidence
- open questions
- next step

A later AI session can resume from the handover rather than replaying the entire conversation history.

### 5. Security Domain First

Route knowledge by:

```text
Security Domain → Project → Feature → Task → Topic
```

Cross-company and cross-domain access is denied by default.

### 6. One Fact, One Source of Truth

Typical ownership rules:

- Human exploration → Human Workspace
- Frozen product decision → Decision Log / Product Contract
- Engineering implementation → GitHub
- Current task → Task Packet
- Implementation evidence → Review Pack
- Repeated workflow failure → Failure Registry

Avoid bidirectional duplication of the same formal fact.

## Human-in-the-loop AI model

KnowYourSelf separates responsibilities rather than asking one model to do everything.

### Owner / Human

Owns:

- intent
- product judgment
- priorities
- visual direction
- security boundaries
- scope freeze
- final acceptance
- release / merge decisions

### Main Agent

A general-purpose reasoning agent such as GPT, Claude, or another capable model handles:

- discovery and clarification
- context routing
- task classification
- contract compilation
- project memory
- implementation handoff
- evidence review
- audit and coaching

### Execution Agent

A coding agent such as **Codex, Claude Code, Cursor Agent, or another coding agent** handles:

- bounded implementation
- tests
- contained self-repair
- evidence
- draft pull requests

An execution agent should not silently change frozen product decisions, cross security boundaries, expand scope, or auto-merge.

## GPT vs Codex: when to use which

Use a general-purpose reasoning model for:

- Discovery
- architecture design
- product decisions
- knowledge management design
- context engineering
- human interviews
- portfolio review

Use Codex or another coding agent after the scope has been compiled into an implementation packet.

Recommended workflow:

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

## Project-level context management

A large software or knowledge project should have a compact **Project Capsule** and, when necessary, smaller **Feature Capsules**.

Example:

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

`PROJECT_ENTRY.md` is a map, not an encyclopedia.

For a feature-level task, load the feature context instead of the entire project.

## Portfolio-level project health

Every active project can publish a thin **Project Health Snapshot** containing:

- green / yellow / red status
- today’s meaningful changes
- pending owner decisions
- pending owner reviews
- risks
- active pull requests
- new regressions versus baseline failures
- context health
- repeated failure patterns
- next step

The portfolio layer consumes these summaries for **daily project reliability audits and weekly portfolio reviews**.

## Two continuous improvement loops

KnowYourSelf separates **project reliability** from **personal growth**.

### Project Reliability Loop

```text
Project Activity
→ Daily Collaboration Audit
→ Failure Registry
→ Rule Promotion
→ Rule Retirement
```

It looks for:

- scope drift
- oversized changes
- wrong Git base/head
- stale context
- design drift
- late visual validation
- excessive Harness / CI checks
- agent permission problems
- repeated PR and workflow failures

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

The AI should not simply ask “What was most valuable today?”. It should inspect observable evidence, propose high-value candidates, and ask a few focused questions.

The goal is to turn daily work into **learning, knowledge, skill, and better judgment**, rather than another passive activity log.

## Typical use cases

### Personal Knowledge Management (PKM)

Build a long-term personal knowledge system without forcing every note, project, file, and code repository into one context.

### Personal AI Operating System

Create a reusable operating model for personal knowledge, projects, learning, reviews, AI agent memory, and long-running work.

### Multi-project AI Agent Management

Run multiple AI-assisted projects while keeping each project's context isolated and allowing a portfolio layer to monitor project health.

### Multi-company Knowledge Management

Use separate security domains for different companies or clients while keeping a unified personal navigation layer.

### Human-in-the-loop Product Development

Keep product intent, decisions, visual direction, and final acceptance with a human owner while AI handles context compilation, planning, execution handoff, and verification.

### AI Coding Agent Workflow

Connect product requirements, design references, task packets, GitHub repositories, tests, review evidence, and session handovers without dumping the entire repository into the prompt.

### Context Engineering for AI Agents

Use progressive disclosure, task-scoped retrieval, project capsules, feature capsules, and session handover to manage AI context size and reliability.

### AI Agent Memory and Persistent State

Separate stable memory, project memory, and session memory so long-running agents do not accumulate irrelevant context.

## Start in 5 minutes

### Step 1 — Choose a reasoning agent

Open [`prompts/BOOTSTRAP_AGENT.md`](prompts/BOOTSTRAP_AGENT.md) and send it to GPT, Claude, Gemini, or another strong reasoning model.

Then say:

> Please read this prompt completely. Enter DISCOVERY only. Do not create Notion pages, databases, automations, or migrate any data yet. Strictly follow Local Detail, Global Summary and No Recursive Context Boot. Ask me only one highest-value question per round.

The first stage is a conversation, not a migration.

### Step 2 — Freeze architecture before implementation

Use:

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

### Step 3 — Start with a small Pilot

Use only:

- Personal HQ
- one personal project
- one knowledge topic
- one company pointer
- one Project Capsule
- one Feature Capsule
- one Project Health Snapshot
- one Session Handover
- one Context Projection example

Do not migrate your entire knowledge archive on day one.

## Recommended tool split

A practical implementation can be:

```text
Notion / Feishu
= Human editing and collaborative knowledge workspace

Google Drive
= Large files, PDFs, datasets, media and backups

GitHub
= Engineering truth, contracts and code

Obsidian (optional)
= Personal Markdown research and offline archive
```

The important rule is not which vendor you choose. The important rules are **one source of truth per fact, clear security boundaries, and controlled agent context**.

## Public repository safety

Never commit:

- API keys
- access tokens
- passwords
- cookies
- private company documents
- private customer data
- private chat exports
- proprietary source code
- secret-bearing URLs
- local machine secrets

This repository contains reusable methodology, templates, schemas, and public examples — not private personal or company information.

## Frequently asked questions

### What is a Personal Knowledge OS?

A Personal Knowledge OS is a structured system for managing personal knowledge, projects, decisions, learning, files, and long-running work across one or more tools. KnowYourSelf adds AI agent context routing and human review to that model.

### Is KnowYourSelf a Notion template?

No. It is a knowledge architecture and AI agent collaboration framework. Notion, Feishu, Google Drive, GitHub, Obsidian, or other tools can implement different layers.

### Is KnowYourSelf only prompt engineering?

No. Prompting is only one layer. The framework focuses on **context engineering, state management, project memory, security domains, project capsules, session handover, evaluation, human review, and continuous workflow improvement**.

### Does an AI agent read my whole knowledge base?

No. The intended architecture uses task-scoped Context Projection. The agent discovers the relevant security domain, project, feature, and evidence as needed.

### Can I use Codex with KnowYourSelf?

Yes. Codex can act as an execution agent after a main reasoning agent has compiled a frozen scope into an implementation packet.

### Can KnowYourSelf manage multiple companies?

Yes, but each company should be a separate security domain. A unified dashboard does not mean unified data access.

### Is KnowYourSelf only for software engineering?

No. The same architecture can manage personal knowledge, research, learning, SaaS product work, projects, and other long-running workflows. Engineering adds a Git-based truth layer rather than replacing the human knowledge layer.

### What problem does Local Detail, Global Summary solve?

It prevents multi-project context explosion. Project details remain local while portfolio-level monitoring operates on small, structured summaries.

### What is a Session Handover?

A compact persistent state artifact that captures the current goal, accepted decisions, implementation status, evidence, open questions, and next step so a later AI session can continue without replaying the entire conversation.

## Documentation

- [`Bootstrap Agent Prompt`](prompts/BOOTSTRAP_AGENT.md)
- [`Highest-Level Principles`](principles/HIGHEST_LEVEL_PRINCIPLES.md)
- [`Owner Quick Start`](docs/OWNER_QUICK_START.md)
- [`Interview State Schema`](schemas/interview_state.yaml)
- [`Project Router Schema`](schemas/project_router.json)
- [`Security Policy`](SECURITY.md)
- [`Contributing Guide`](CONTRIBUTING.md)
- [`Changelog`](CHANGELOG.md)

## Language versions

- **English (default):** `README.md`
- [简体中文](README.zh-CN.md)
- [繁體中文](README.zh-TW.md)

## Search topics

KnowYourSelf is intended to be useful for people researching **personal knowledge management, PKM, personal AI operating systems, AI knowledge bases, AI agent memory, persistent AI memory, agent context management, context engineering, context window management, human-in-the-loop AI, multi-agent workflows, AI coding agents, Codex workflows, Claude Code workflows, project context, project memory, session handover, AI agent orchestration, Notion knowledge management, Obsidian knowledge management, GitHub AI workflows, prompt engineering, agent reliability, AI workflow automation, project health monitoring, Failure Registry, knowledge governance, portable AI memory, and multi-company knowledge management**.

## License

MIT. See [`LICENSE`](LICENSE).
