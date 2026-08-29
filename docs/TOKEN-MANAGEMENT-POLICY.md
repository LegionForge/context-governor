# LegionForge Token-Management Policy

Status: draft v0.1  
Owner: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org  
Effective date: 2026-08-28 America/Chicago

## Purpose

Keep unnecessary context and compute out of AI work without trading away correctness or forcing repeated work. Token usage is an operational signal, not a success metric by itself.

## Normative rules

The words MUST, MUST NOT, SHOULD, and MAY are requirements for LegionForge workflows.

### R1 — Measure before tuning

For any recurring workflow, record the task, model/harness, input size, output size, retries, review time, and outcome before changing it. A proposed saving is not accepted from token count alone.

Acceptance requires: no material increase in errors, retries, review time, or repeated work; and a before/after record for the same task class.

### R2 — Keep only decision-relevant context

An agent MUST receive the smallest set of files, messages, tool definitions, and prior decisions needed for the current task. It MUST NOT receive an entire document, repository, log, or conversation when a scoped slice is sufficient.

The requester or orchestrator SHOULD state the relevant paths, ranges, symbols, or decision IDs. The agent SHOULD search first and read narrowly.

### R3 — Correct in place; do not debate avoidable mistakes

When the user notices a factual or instruction error, the workflow SHOULD edit or replace the erroneous instruction/artifact in place when the interface supports it. It MUST NOT create a long corrective back-and-forth merely to preserve a bad branch.

If in-place correction is unavailable, the agent MUST start a replacement task with a concise correction and a pointer to the authoritative artifact.

### R4 — Compress deterministic material before model review

Raw logs, JSON, command output, and repeated reports MUST be filtered, summarized, or structurally compressed before entering model context when the transformation preserves the evidence needed for the task. Originals MUST remain recoverable outside the prompt.

Compression MUST be task-aware: never remove lines needed to diagnose the issue, verify a claim, or reproduce a failure.

### R5 — Prune ambient configuration

Unused MCP/connectors, skills, plugins, lengthy skill descriptions, and stale project instructions MUST be disconnected, archived, shortened, or scoped out of the active workflow. Configuration that is always loaded MUST earn its context cost through repeated use.

Project instructions SHOULD be split into narrowly applicable files or rules when one global document is causing unrelated work to carry irrelevant context.

### R6 — Use the minimum viable model and harness

Each repeatable skill SHOULD declare its minimum viable model and harness for the task. Route deterministic execution (edit, run, format, test, collect evidence) to the leanest reliable path; reserve stronger reasoning paths for judgment, ambiguity, or high-risk review.

Changing model or harness is a controlled experiment: preserve the task and acceptance checks, change one knob, and compare outcome quality as well as usage.

### R7 — Checkpoint and reset at a state boundary

At a natural milestone, the workflow MUST save the goal, decisions, changed files, test results, unresolved risks, and next action to durable project artifacts. It SHOULD then use a fresh session when accumulated history is no longer decision-relevant.

No reset is allowed to discard the only copy of a decision, failure, or acceptance result.

### R8 — Treat caching and reused input honestly

Cached or reused input MUST still be counted as context carried by the workflow. It MUST NOT be described as free, useless, or proof of waste without provider-specific billing evidence.

Reports MUST distinguish local estimates, provider-reported usage, and billable usage.

### R9 — Escalate only with evidence

Before adopting a major change—router, provider switch, local model, or multi-agent redesign—the owner MUST show the measured bottleneck and define a rollback and quality benchmark. A larger context window is not a substitute for context hygiene.

### R10 — Cache keepalive is opt-in and bounded

For Anthropic workflows that explicitly use prompt caching, a keepalive MAY be tested during a short planned pause to preserve cache locality. It MUST be provider-specific, tool-free, time-bounded, and disabled when the work resumes, the cache window expires, or the measured savings do not exceed the keepalive request cost.

Example experiment: `/loop 3m "Cache keepalive only. Do not run tools. Reply only: keepalive"`.

The run record MUST include cache writes, cache hits/refreshes, keepalive requests, total input/output, and billable cost where available. Keepalives MUST NOT be used to evade budgets, keep a session alive indefinitely, or imply that cached input is free. Anthropic's current pricing documentation lists a default 5-minute cache and separate pricing for cache hits/refreshes; verify provider behavior before automating this rule.

### R11 — Stabilize cache-sensitive session configuration

At session start, choose the least costly model, effort/reasoning level, and tool set that can satisfy the acceptance test. The workflow SHOULD keep those choices stable for the session. If a change is necessary, record it as a new cache epoch and re-measure; do not assume a cheaper model switch is cheaper when it invalidates a large cached prefix.

### R12 — Delegate only when the whole-session math pays back

Before spawning a subagent, estimate its startup context, memory/instruction load, tool schemas, work input, result size, and the main-session turns that will reuse the result. Delegate when the avoided repeated context and isolation benefit exceed that overhead and the handoff can be verified. A shorter summary in the parent context is not sufficient evidence of savings.

### R13 — Govern unattended work as live spend

Scheduled jobs, loops, keepalives, and agent teams MUST have an owner, purpose, maximum duration or run count, attached-context size, stop condition, and usage record. They MUST stop when the task is complete or the budget is reached. A session left open is not equivalent to an actively consuming loop; audit actual invocations and child-agent lifetimes.

## Enforcement levels

| Level | Mechanism | Examples |
|---|---|---|
| Required gate | Reject the run or review until satisfied | missing task scope, missing acceptance check, destructive context pruning without recovery |
| Automated check | Lint, hook, or dashboard warning | oversized raw output, unbounded output, unused integration inventory |
| Workflow default | Agent/orchestrator behavior | narrow retrieval, terse output, checkpoint at milestone |
| Advisory | Human review and experiment backlog | model routing, local runtime, cache keepalive |

## Minimum run record

Every benchmark or production experiment MUST record:

- task class and acceptance test;
- model, harness, and relevant configuration knobs;
- input/output token estimates, if available, plus their source;
- retries, failures, review time, and repeated work;
- quality result and reviewer/date;
- context removed and why it was safe to remove;
- rollback path.

Cache experiments MUST additionally record cache writes, hits/refreshes, keepalive count, and provider billing fields.

## Default thresholds

These are starting controls, not universal truths. Tune one value per experiment and re-run the safety/quality checks.

- Warn when a single injected artifact exceeds 8,000 estimated tokens.
- Warn when an output contract does not specify a maximum or structured format.
- Require a checkpoint before starting a new task after 20 conversational turns or after a major milestone, whichever comes first.
- Require a monthly usage review for recurring workflows.
- Block a claimed optimization if errors, retries, review time, or repeated work rise by more than 5% without explicit owner approval.
- Do not schedule cache keepalives beyond the declared pause window.
- Require a cache-epoch record when model, effort, tool set, sandbox, or working directory changes mid-session.
- Do not spawn a subagent without an estimated overhead and a parent-session handoff target.
- Do not run unattended work without an owner, stop condition, and bounded budget.

## Exceptions

An exception is allowed only when extra context is required for correctness, safety, legal/compliance review, or reproducibility. Record the reason, retained context, approver, and expiry/review date. Exceptions do not waive measurement or recovery requirements.

## What this policy does not claim

It does not promise a fixed percentage reduction, control hidden platform context, or establish provider billing from local counters. Nate's reported 90% target is a test target, not a LegionForge guarantee.

## Sources and evidence boundary

- Source-backed: Nate describes a 3.77 billion-token local tracker day, 95.73% reported reused input, and explicitly frames those numbers as a signal rather than a bill; he also states the goal of reducing reused input without increasing mistakes, retries, review time, or repeated work.
- Transcript-indexed: the video summary identifies usage auditing, editing errors in place, pruning unused skills/MCPs, compressing inputs, minimum-viable models, routing execution work to a leaner harness, and checkpointing/resetting as the relevant practices.
- Provider-backed: Anthropic's pricing documentation describes 5-minute and 1-hour prompt-cache durations and separate cache-hit/refresh pricing.
- Project decision: the MUST/SHOULD language, thresholds, run record, and enforcement levels above are LegionForge's proposed controls and require validation against real workloads.

See the [field note](field-notes/2026-08-28-token-management.md) for the evidence ledger and transfer decisions.
