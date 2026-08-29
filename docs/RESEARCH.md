# Context-saving research brief

Date: 2026-08-28 America/Chicago  
Scope: long development sessions with many tool calls  
Author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org

## Findings that transfer

### 1. Context selection beats stylistic terseness

Anthropic describes context engineering as selecting the smallest high-signal token set, and recommends efficient tool contracts, scoped context, and testing a minimal prompt before adding complexity. Its Claude Code documentation also distinguishes always-loaded instructions, on-demand skills, isolated subagents, and zero-context-cost hooks. This supports a portable contract with thin always-on rules and external enforcement.

Sources: [Anthropic context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), [Claude Code extension model](https://code.claude.com/docs/en/features-overview)

### 2. Tool output is a primary long-session hazard

Claude Code warns when MCP output exceeds 10,000 tokens and exposes a configurable maximum. The portable rule should cap repetitive output, retain exact evidence externally, and return a pointer or structured digest to the main session.

Source: [Claude Code MCP output limits](https://code.claude.com/docs/en/mcp)

### 3. Compaction should be a checkpoint, not a blind summary

Codex explains that tool calls append to the prompt and that context grows across turns; its agent loop automatically compacts after a configured limit. OpenCode documents structured checkpoints with an objective, work state, blockers, next moves, and a recent tail. Hermes exposes a pluggable `ContextEngine`, separate pre-agent and in-loop compression, token tracking, and optional lossless engines. These all support a shared checkpoint schema plus provider-native compaction.

Sources: [OpenAI Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/), [OpenCode compaction](https://opencode.ai/v2/docs/compaction/), [Hermes context compression](https://hermes-agent.nousresearch.com/docs/developer-guide/context-compression-and-caching/)

### 4. Lossless recall is the right escape hatch for high-risk evidence

Hermes's documented context-engine interface separates per-request selection from persisted history, while Hermes-LCM preserves raw messages and lets the agent recover exact detail after compaction. This is preferable to forcing one lossy summary to carry every debugging fact.

Sources: [Hermes context-engine plugin](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/developer-guide/context-engine-plugin.md), [Hermes-LCM](https://github.com/stephenschoettler/hermes-lcm)

### 5. Caveman-style output compression is useful but not a universal win

Caveman reports a 65% average output reduction in its own benchmark, while also documenting an added roughly 1–1.5k tokens per turn for the injected skill. JetBrains' independent paired test found much smaller savings in its tested workload and highlighted quality/cost tradeoffs. The transferable idea is concise output contracts and minimal narration—not forced low-information language or a promised savings percentage.

Sources: [Caveman honest numbers](https://github.com/JuliusBrussee/caveman/blob/main/docs/HONEST-NUMBERS.md), [JetBrains benchmark](https://blog.jetbrains.com/ai/2026/07/speak-to-ai-agents-like-cavemen-tosave-tokens/)

### 6. Persistent memory should be structured and selective

OpenAI describes retrieval of only relevant context instead of scanning raw metadata or logs, and emphasizes carrying learnings forward through memory. For development sessions, durable checkpoints and decision records should be indexed, while raw tool traces remain recoverable but out of the active prompt.

Source: [OpenAI internal data agent](https://openai.com/index/inside-our-in-house-data-agent/)

## Recommended portable architecture

`context contract -> surface adapter -> external evidence store -> checkpoint -> native compaction/retrieval`

The contract is natural language because every surface can consume it. The adapter is where enforcement lives: hooks can block or log without adding context, skills can guide judgment, and native context engines should own provider-specific compaction.

## Open questions for the benchmark

- Does a deterministic output filter reduce total session tokens after accounting for re-fetches?
- Does lossless recall reduce retries versus a provider-native summary on debugging tasks?
- Which tool-output cap preserves enough evidence for tests, logs, and browser traces?
- When does a cache keepalive cost more than the cache-hit savings?
- Does concise narration improve throughput without hiding important state?

## Provenance stamp

AI tool: OpenAI Codex via API  
Provider: OpenAI  
Model ID: not exposed in session metadata  
AI role: multi-source research synthesis and architecture drafting  
Human author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org  
Created/revised: 2026-08-28 America/Chicago
