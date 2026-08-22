# Contributing to KnowYourSelf

Thanks for helping improve KnowYourSelf.

This repository is intentionally evolving. The goal is not to freeze one perfect Knowledge OS, but to publish a small, testable set of principles, prompts, schemas, and workflows that can improve through real-world use.

## Before you contribute

Please read:

1. `README.md`
2. `principles/HIGHEST_LEVEL_PRINCIPLES.md`
3. `prompts/BOOTSTRAP_AGENT.md`

The most important design constraint is:

> Local Detail, Global Summary.

A contribution should improve the system without making the global context heavier than necessary.

## What belongs here

Good contributions include:

- improvements to the Bootstrap prompt;
- clearer context-routing rules;
- better Project / Feature Capsule patterns;
- migration and portability patterns;
- human-in-the-loop workflows;
- Daily Audit / Personal Compounding mechanisms;
- reusable schemas and examples;
- failure patterns backed by real evidence;
- documentation that makes the system easier for a new user or agent to adopt.

## What does not belong here

Do not submit:

- private company documents;
- private chat exports;
- credentials or secrets;
- proprietary code;
- customer data;
- private repository URLs containing sensitive information;
- personal data that is not necessary to explain a reusable pattern.

## Issue vs Pull Request

Use an **Issue** when you want to:

- report a confusing instruction;
- propose a new mechanism;
- document a failure pattern;
- discuss an architectural trade-off;
- suggest a new example.

Use a **Pull Request** when the intended change is sufficiently clear and you can provide a concrete patch.

For ambiguous architectural changes, open an Issue first.

## Pull Request expectations

A good PR should explain:

- **Problem** — what was confusing, broken, or missing;
- **Evidence** — how you know this matters;
- **Change** — exactly what changed;
- **Scope** — what is intentionally not changed;
- **Compatibility** — whether existing prompts, schemas, or workflows remain valid;
- **Context impact** — whether the change increases default context size or retrieval scope;
- **Migration** — whether users need to update existing installations.

## Keep the harness light

Do not add a permanent automation rule merely because one failure occurred.

Prefer:

```text
Observation
→ Failure Pattern
→ Repetition Check
→ Main Agent Rule
→ Preflight Rule
→ Harness Rule
```

Only promote a rule when it is repeatedly useful, reliably detectable, and worth its maintenance cost.

## Context discipline

Contributions must preserve these invariants:

- no recursive root context boot;
- no default cross-project context loading;
- no default cross-company access;
- historical material is retrieved on demand;
- Failure Registry entries are injected selectively;
- long sessions can be compressed into persistent state.

## Documentation style

Prefer:

- concrete examples over abstract slogans;
- explicit state transitions;
- small reusable templates;
- clear owner/agent responsibility boundaries;
- Chinese or English content when it materially improves usability.

Avoid:

- giant prompt dumps with no structure;
- duplicated rules across many files;
- instructions that require the Owner to solve machine-level problems;
- process for process' sake.

## Versioning

When a change modifies the behavior of the Bootstrap prompt or a schema, update `CHANGELOG.md`.

For materially incompatible changes, call them out explicitly under an `Unreleased` or versioned heading.
