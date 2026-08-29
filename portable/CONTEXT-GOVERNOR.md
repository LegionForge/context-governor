# Context governor

Apply these rules during long development sessions.

## Before a tool call

- State the immediate decision or artifact the call must support.
- Search or inspect metadata before reading large files.
- Read the narrowest path, range, symbol, or record that can answer the question.
- Prefer a child session for a large independent read; return a result, paths, and evidence IDs—not the raw corpus.

## When handling tool output

- Cap repetitive output and summarize deterministic material before it re-enters the main context.
- Preserve the original output on disk or in a durable store when it may be needed for verification or recovery.
- Keep errors, timestamps, commands, changed paths, and reproduction data exact.
- Never hide uncertainty by replacing missing evidence with a confident summary.

## During the task

- Keep narration concise; use structured output when another agent or hook consumes it.
- Do not repeat a correction as a debate. Update the authoritative artifact and continue from it.
- Do not add unrelated tools, skills, MCP servers, plugins, or instructions to the active session.
- Treat model, harness, context threshold, and keepalive interval as separate knobs. Change one at a time.
- Choose model, effort, and tools before the session; keep them stable unless a recorded cache epoch is worth the switch.
- Before spawning a child agent, estimate its startup/context overhead and the parent turns it will replace.
- Treat loops, schedules, keepalives, and live agent teams as running work: require an owner, budget, and stop condition.

## At a milestone or context boundary

Write a checkpoint that satisfies `checkpoint.schema.json`, then compact, delegate, or start a fresh session. A checkpoint is not a transcript: it is a durable index into the transcript and artifacts.

The checkpoint must include:

- objective and acceptance tests;
- decisions and constraints that must survive compaction;
- changed files and current status;
- exact evidence paths/IDs and test results;
- blockers, risks, and the single next action.

## Quality gate

A context reduction is successful only if the task still passes its acceptance test without a material increase in errors, retries, review time, or repeated work. Report local estimates separately from provider-reported or billable usage.
