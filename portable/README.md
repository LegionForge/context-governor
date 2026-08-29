# Portable Context Governor

This bundle is the provider-neutral layer for Codex, Claude Code, Hermes, Row-Bot, and OpenCode.

It has three parts:

1. `CONTEXT-GOVERNOR.md` — short natural-language behavior rules. Put this in a project instruction file or invoke it as a skill.
2. `context-policy.yaml` — shared thresholds and enforcement intent for adapters.
3. `checkpoint.schema.json` — the durable handoff contract used before compaction, reset, or delegation.

The contract is intentionally small. It governs what context should be selected and what state must survive; it does not attempt to replace each surface's native compaction engine.

## Adapter map

| Surface | Best integration point | First enforcement |
|---|---|---|
| Codex | project `AGENTS.md` plus a local checkpoint command | instruction + durable checkpoint |
| Claude Code | `CLAUDE.md`/on-demand skill, `PreCompact`, `SessionStart`, and `PreToolUse` hooks | hooks for logging/blocking; skill for judgment |
| Hermes | `ContextEngine` plugin/config plus context references | native compressor/LCM + selected retrieval |
| Row-Bot | profile/orchestrator policy and checkpoint-safe child budgets | profile policy + bounded child sessions |
| OpenCode | `opencode.json` compaction config and plugin hooks | automatic compaction + context hook |

Keep the governor text under roughly 100 lines and do not load it globally in every surface unless the cost has been measured. The policy is most valuable at task start, tool-result boundaries, compaction, and session handoff.

## Portable invocation

Use this natural-language instruction when a surface has no hook or skill system:

> Act as the context governor for this development task. Search before reading, request only decision-relevant files, cap or summarize deterministic tool output, and keep exact evidence recoverable by path or identifier. At a milestone or before context compaction, write a checkpoint containing objective, acceptance tests, decisions, changed files, evidence, blockers, and next action. Be concise in narration, but never omit safety, correctness, or reproducibility details. If unsure whether context is safe to drop, preserve it externally and reference it rather than guessing.

## Provenance

AI tool: OpenAI Codex via API  
Provider: OpenAI  
Model ID: not exposed in session metadata  
AI role: research synthesis and implementation design  
Human author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org  
Created/revised: 2026-08-28 America/Chicago
