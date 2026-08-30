# Developer context management: 2026 R&D note

Date: 2026-08-29 America/Chicago  
Status: research backlog, not a validated benchmark  
Author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org

## Scope

This note surveys current first-party guidance for developer-facing coding
agents. It extends the source register; it does not replace the two Nate B.
Jones source videos that motivated this project.

## Findings

### 1. Repository knowledge should be the system of record

OpenAI's harness-engineering report describes replacing a large instruction
manual with a navigable map of plans, decisions, architecture, and quality
grades. The practical implication is to keep durable project truth in small,
owned artifacts and make the agent retrieve the relevant slice.

Source: [OpenAI harness engineering](https://openai.com/index/harness-engineering/)

### 2. Prefer just-in-time retrieval to front-loading everything

Anthropic's context-engineering guidance recommends lightweight identifiers
such as file paths, stored queries, and links, with agents loading details via
tools when needed. This reduces context pollution while preserving access to
evidence.

Source: [Anthropic effective context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

### 3. Treat compaction as a state transition

OpenAI describes automatic compaction when a threshold is exceeded and a
compact representation is substituted for the prior input. Anthropic presents
compaction, structured note-taking, and multi-agent architecture as separate
long-horizon techniques. A developer workflow should therefore checkpoint
before compaction and retain exact artifacts outside the active context.

Sources: [OpenAI Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/),
[Anthropic long-running harnesses](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

### 4. Tool design is context design

Anthropic recommends a minimal viable tool set and concise, high-signal tool
contracts. For developer agents, tool output should have bounded size,
structured fields, stable identifiers, and a recoverable raw artifact when the
full output matters.

Source: [Anthropic effective context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

### 5. Long-running work needs explicit continuity artifacts

OpenAI's Codex guidance emphasizes persistent workspace practices for work
beyond one prompt. The recommended developer primitive is a small current-state
record containing objective, acceptance checks, decisions, blockers, evidence
paths, and next action, with history kept separately.

Source: [OpenAI Codex-maxxing for long-running work](https://openai.com/index/codex-maxxing-long-running-work/)

## Proposed experiments

These are hypotheses for LegionForge validation, not claims of measured gains:

1. Compare a monolithic instruction file with a map plus current-state file on
   matched coding tasks; measure correctness, retries, review time, and input
   tokens.
2. Compare front-loaded repository context with just-in-time path retrieval;
   record missed facts, tool calls, and total context carried.
3. Compare opaque summarization with checkpoint-before-compaction; test whether
   exact evidence recovery reduces rework on debugging tasks.
4. Measure tool contracts with bounded structured output against raw command
   output, including the cost of fetching the preserved full artifact.
5. Test one configuration knob per iteration and re-run the safety/acceptance
   checks after every change.

## Decision boundary

Adopt a technique as a project default only after a matched-task benchmark shows
no material regression in correctness, retries, review time, or repeated work.
Report local token estimates separately from provider-reported and billable
usage. Preserve raw evidence and the benchmark record outside the active model
context.

## Provenance stamp

AI tool: OpenAI Codex via API  
Provider: OpenAI  
Model ID: not exposed in session metadata  
AI roles: primary-source research synthesis and experiment design  
Human author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org  
Created/revised: 2026-08-29 America/Chicago

