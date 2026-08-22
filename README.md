# KnowYourSelf — Knowledge OS Bootstrap

A vendor-neutral bootstrap kit for building a personal Knowledge OS around human-in-the-loop AI collaboration.

> **Local Detail, Global Summary.**

Projects keep detailed context locally. The portfolio layer consumes compact project snapshots. Agents load the smallest context required for the current task instead of recursively loading an entire knowledge base.

## Why this exists

Most AI workflows fail in one of two directions:

- the human becomes a prompt engineer who has to describe the entire world every time;
- the agent receives too much context, too much authority, and too little structure.

KnowYourSelf explores a third model:

```text
Human intent
    ↓
Main Agent
    ↓
Context routing + task compilation
    ↓
Execution Agent
    ↓
Evidence + review
    ↓
Persistent project state
```

The goal is not maximum automation. The goal is **reliable leverage** while keeping the human in control of decisions, boundaries, and acceptance.

## Start in 5 minutes

### 1. Use the Bootstrap Prompt with a general-purpose reasoning agent

Open:

`prompts/BOOTSTRAP_AGENT.md`

Then tell the agent:

> Please read this prompt completely. Enter DISCOVERY only. Do not create Notion pages, databases, automations, or migrate any data yet. Strictly follow Local Detail, Global Summary and No Recursive Context Boot. Ask me only one highest-value question per round.

The first phase is a conversation, not a migration.

### 2. Do not let the agent jump directly to implementation

Use this lifecycle:

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

### 3. Start with a small Pilot

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

Run the pilot before expanding.

## Core principles

### Local Detail, Global Summary

Project details stay inside the project. The global layer normally consumes only health, pending owner decisions/reviews, risks, cross-project failure patterns and next steps.

### No Recursive Context Boot

Never do:

```text
Root → all companies → all projects → all knowledge → all history → current task
```

Prefer:

```text
Global Minimal → Security Domain → Project → Feature → Task → Relevant evidence
```

### Knowledge Available ≠ Context Loaded

A document can be searchable without being injected into every prompt. Distinguish AVAILABLE / SEARCHABLE / READABLE / LOADED / WRITABLE.

### Conversation is Ephemeral; State is Persistent

Long sessions should produce `SESSION_HANDOVER.md`. Resume from the handover instead of replaying the entire conversation.

### Security Domain First

Route by `Security Domain → Project → Feature → Task → Topic`. Cross-domain and cross-company access is denied by default.

### Project Autonomy, Portfolio Governance

Projects own their details. Portfolio governance only consumes thin summaries such as health, risk, pending decisions/reviews, repeated failures and next steps.

## Human-in-the-loop model

**Owner:** intent, judgment, product decisions, visual direction, security boundaries, scope freeze, acceptance, release/merge.

**Main Agent:** context routing, discovery, task classification, contract compilation, evidence review, agent dispatch, audit and coaching.

**Execution Agent:** bounded implementation, tests, contained self-repair, evidence and draft PR.

The execution agent must not silently change product contracts, cross security domains, expand scope or auto-merge.

## GPT vs Codex

Use a general-purpose reasoning agent for Discovery and architecture. Use Codex or another coding agent only after the scope is frozen and an Implementation Packet exists.

```text
General-purpose Main Agent
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
```

## Repository structure

```text
KnowYourSelf/
├── README.md
├── LICENSE
├── SECURITY.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── prompts/
│   └── BOOTSTRAP_AGENT.md
├── principles/
│   └── HIGHEST_LEVEL_PRINCIPLES.md
├── docs/
│   └── OWNER_QUICK_START.md
├── schemas/
│   ├── interview_state.yaml
│   └── project_router.json
├── archive/
│   └── v2/                 # historical bootstrap snapshot
└── .github/
    └── ISSUE_TEMPLATE/
```

## How to contribute

Read `CONTRIBUTING.md` before opening a pull request.

Use an **Issue** for a new architecture idea, failure pattern, unclear behavior, or discussion that still needs exploration.

Use a **Pull Request** when the change is sufficiently understood and you can provide a focused patch.

Good contributions should explain the problem, evidence, proposed change, scope, context impact, alternatives, and migration cost.

## Design philosophy for contributions

This project intentionally resists “more process = more reliability.”

A new rule, hook, harness check, or required document should only be added when there is evidence that it addresses a repeated or high-cost failure and the machine can enforce it with acceptable false positives.

Prefer:

```text
Observation
→ Failure Pattern
→ Repetition Check
→ Main Agent Rule
→ Preflight Rule
→ Harness Rule
→ Retirement when no longer needed
```

## Public repository safety

Do not commit:

- API keys
- access tokens
- passwords
- cookies
- private keys
- private company documents
- private customer data
- private chat exports
- proprietary source code
- secret-bearing URLs

This repository contains public methodology and reusable templates, not private personal or company data. See `SECURITY.md` for the project security policy.

## License

MIT. See `LICENSE`.

## Status

This project is intentionally **experimental and iterative**. The architecture is expected to evolve through actual use. Historical snapshots are preserved so that design decisions and revisions remain inspectable.
