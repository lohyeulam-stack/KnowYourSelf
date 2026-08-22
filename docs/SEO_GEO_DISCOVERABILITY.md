# SEO and GEO Discoverability Guide

## Purpose

This document explains how KnowYourSelf is written and organized so that both traditional search engines and generative AI systems can understand the project.

The goal is not keyword stuffing. The goal is to make the project **clear, specific, useful, original, and easy to cite**.

## Primary topic

The primary topic of this repository is:

> **A federated Personal Knowledge OS and human-in-the-loop AI agent workflow for context engineering, project memory, and multi-project knowledge management.**

## Core concepts

Use these concepts consistently when they are genuinely relevant:

- Personal Knowledge Management (PKM)
- Personal AI Operating System
- AI knowledge base
- AI agent memory
- persistent AI memory
- context engineering
- AI context management
- context window management
- human-in-the-loop AI
- AI coding agents
- multi-agent workflows
- AI agent orchestration
- project context
- project memory
- session handover
- project health snapshot
- security domains
- source of truth
- failure registry
- workflow reliability
- Notion knowledge management
- Obsidian knowledge management
- GitHub AI workflow
- Codex workflow

## Search-intent pages

Future documentation should be organized around real questions and use cases instead of creating pages only to target a keyword.

Recommended topics include:

- What is a Personal Knowledge OS?
- How should AI agents manage project context?
- How do you prevent AI agent context explosion?
- How should multiple projects share knowledge without sharing all context?
- How should you separate Notion, Google Drive, and GitHub in an AI workflow?
- How should GPT and Codex work together?
- What is a Session Handover for AI agents?
- What is Context Projection?
- How should a portfolio-level AI agent monitor many projects?
- How do you manage AI agent memory across long-running projects?

## GEO / generative search writing rules

### Answer first

A page should clearly answer its main question near the top. Do not hide the core definition inside a long introduction.

### Use explicit entities

Prefer concrete terms such as:

- Personal Knowledge OS
- Notion
- Google Drive
- GitHub
- Codex
- Claude Code
- Project Capsule
- Session Handover
- Context Projection
- Project Health Snapshot

Avoid vague language such as “the system”, “the tool”, or “the workflow” when the specific entity is known.

### Define specialized terms

The first useful occurrence of a project-specific term should include a plain-language definition.

Example:

> **Project Health Snapshot** is a compact machine-readable summary of a project's current status, risks, pending decisions, reviews, regressions, and next step.

### Prefer evidence and examples

Pages should contain:

- concrete examples
- explicit workflows
- small schemas
- diagrams written in text
- limitations
- trade-offs
- failure cases

The project should describe what it actually does rather than make broad claims about AI.

### Keep concepts internally consistent

If “Local Detail, Global Summary” is used as a core principle, all documentation should preserve the same meaning:

> project-level detail, portfolio-level summary, task-scoped context.

### Build topic clusters

The README is the hub.

Supporting pages should form a semantic cluster around:

```text
Personal Knowledge OS
├── Human Knowledge Layer
├── Engineering Truth Layer
├── Agent Context Layer
├── Project Capsules
├── Feature Capsules
├── Context Projection
├── Session Handover
├── Project Reliability Loop
├── Personal Compounding Loop
└── Migration / Security / Governance
```

### Link concepts explicitly

Related pages should link to each other with descriptive anchor text rather than generic links such as “click here”.

## What not to do

Do not:

- repeat the same keyword hundreds of times;
- generate thin pages for every keyword variation;
- publish generic AI content unrelated to the repository;
- make unsupported claims about ranking, indexing, or model behavior;
- create fake FAQ questions solely to place keywords;
- copy vendor documentation as a substitute for original analysis.

## Evidence and provenance

When a document makes a technical or strategic claim, prefer:

1. primary documentation;
2. first-party engineering posts;
3. repository examples;
4. reproducible tests;
5. clearly labeled opinion.

When content is derived from external sources, preserve the source link and distinguish quotation, evidence, and interpretation.

## Versioning

SEO/GEO copy is part of the product surface and should change when the architecture changes.

When a core term changes, update:

- README
- relevant documentation
- examples
- glossary/FAQ
- changelog

## Review checklist

Before merging a documentation change, ask:

- Does the page have a clear primary question or topic?
- Is the answer explicit near the top?
- Are the entities named precisely?
- Are specialized terms defined?
- Does the page include unique evidence or examples?
- Are related concepts linked?
- Is the wording useful to a human reader without search keywords?
- Are claims supported or clearly labeled as recommendations?
- Could another AI system quote this page without losing the meaning?
