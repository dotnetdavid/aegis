# Aegis

![Aegis: governed AI-assisted software delivery](assets/aegis-hero.png)

> Canonical Codex skill identifier: `aegis`. The project folder remains `ai-sdlc` for continuity.

## Executive Overview

Aegis turns AI-assisted development into a disciplined, evidence-led workflow that still moves at practical speed. Unlike an unchecked prompt-to-code approach or a heavyweight one-size-fits-all process, it scales planning, verification, and human approval to the risk of the work. Leaders get clearer decisions, stronger release confidence, and a durable record of why the project is worth doing.

### Who

Codex users and their human decision makers use this skill. Codex acts as the project manager (PM), with a principal-engineer mindset. The human in the loop (HITL) owns consequential approvals.

### What

`aegis` is a Codex skill for running an AI-assisted software development lifecycle. It helps projects create durable memory, govern AI grounding as an evidence dependency, assess risk, build a specification and build package, govern implementation agents, validate evidence, and stop for human approval at consequential decisions.

### When

Use it when a user explicitly invokes `aegis`. When a request clearly needs durable development governance but does not name the skill, Codex asks whether to use it before activating the workflow.

### Where

The authoritative source is `skill/aegis/` in this project. A reviewed copy is promoted to Codex's runtime skill directory only after approval and verification.

### Why

AI can accelerate development, but it cannot own product decisions, security boundaries, acceptance, or release responsibility. This skill keeps evidence and human accountability at the center while scaling process to consequence.

## V1 Boundary

V1 delivers a Codex skill, Markdown lifecycle guidance, reusable Markdown templates, durable artifact maintenance, grounding-governance guidance, and verified runtime promotion. It does not deliver a CLI, dashboard, external integration, automated indexing service, or automated enforcement layer.
