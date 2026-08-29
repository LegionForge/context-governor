---
name: legionforge-context-governor
description: Govern long, tool-heavy development sessions by selecting narrow context, controlling tool output, preserving recoverable evidence, checkpointing before compaction or reset, and measuring quality-adjusted token savings. Use when a coding task involves many tool calls, large files or logs, delegation, cache-sensitive configuration, or unattended work.
license: Apache-2.0
metadata:
  author: LegionForge
  version: "0.1.0"
  repository: https://github.com/LegionForge/legionforge-context-governor
---

# LegionForge Context Governor

Use this skill to control context growth without hiding evidence or reducing verification quality.

## Before reading or calling tools

- State the immediate decision or artifact the call must support.
- Search or inspect metadata before reading large files.
- Request only the smallest path, range, symbol, or record that can answer the question.
- Prefer an isolated child agent for a large independent read; return a verified result, paths, and evidence IDs—not the raw corpus.

## Tool output and evidence

- Cap repetitive output and summarize deterministic material before it re-enters the main context.
- Preserve the original output in a recoverable file or store when it may be needed for verification or reproduction.
- Keep commands, timestamps, errors, changed paths, and reproduction data exact.
- If evidence is uncertain, preserve it and say what remains unverified.

## Session discipline

- Keep narration concise, but never omit safety, correctness, or reproducibility details.
- Do not turn corrections into a long debate; update the authoritative artifact and continue from it.
- Do not add tools, skills, connectors, or instructions to the active session unless the task needs them.
- Choose model, effort, and tools before the session. Record a cache epoch if any cache-sensitive setting changes.
- Before delegating, estimate child startup/context overhead and the parent turns the result will replace.
- Treat loops, schedules, keepalives, and agent teams as active work with an owner, budget, and stop condition.

## Checkpoint boundary

Before compaction, reset, handoff, or a natural milestone, write a checkpoint conforming to [references/checkpoint-schema.json](references/checkpoint-schema.json). It must include the objective, acceptance tests, status, decisions, changed files, exact evidence paths or IDs, test results, blockers, risks, and one next action.

A checkpoint is an index into durable artifacts, not a replacement for raw evidence. If dropping context could affect debugging, security, or reproducibility, store it externally and reference it.

## Quality gate

Call a reduction successful only when the acceptance test still passes without a material increase in errors, retries, review time, or repeated work. Distinguish local estimates, provider-reported usage, cache hits, and billable usage.
