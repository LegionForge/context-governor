# Field note: token management policy seed

Date: 2026-08-28 America/Chicago  
Author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org

## Problem

AI sessions can carry much more than the newest user sentence: prior exchanges, instructions, tool definitions, files, screenshots, command output, and rejected branches. A short visible prompt can therefore trigger a large reused-input payload.

## Evidence

- Nate B. Jones reports 3.77 billion tokens in one local Codex tracker day; 3.59 billion of 3.75 billion input tokens were reported as reused (95.73%). He cautions that this was a local event log, not an OpenAI bill. Source: https://natesnewsletter.substack.com/p/reduce-ai-token-usage
- The same article sets an explicit experiment target: reduce reported reused input by 90% without increasing mistakes, retries, review time, or repeated work. Source: https://natesnewsletter.substack.com/p/reduce-ai-token-usage
- The indexed transcript summary for the supplied video identifies these mechanisms: inspect usage; edit errors in place; remove unused skills/MCPs and shorten descriptions; scope input instead of pasting whole documents; compress deterministic outputs; set a minimum viable model for repeatable skills; route execution to a leaner harness; checkpoint and start fresh at a state boundary. Source: https://engineeringsignals.com/item/2026-W31/youtube-natebjones-001.md
- Anthropic's pricing documentation currently describes 5-minute and 1-hour prompt-cache durations and separate pricing for cache hits/refreshes. Source: https://docs.anthropic.com/en/docs/about-claude/pricing

## Mechanism

The most transferable control is context hygiene: make relevance explicit, reduce deterministic ballast before model review, and preserve only the state needed for the next decision. Model choice, harness choice, and cache strategy can multiply the effect, but they should follow measurement rather than precede it.

## Transfer decisions

1. Adopt quality-adjusted savings as the project objective. Token reduction without quality checks can increase retries or repeated work.
2. Encode narrow-context retrieval, compression, pruning, and checkpointing as defaults because they can be applied across providers.
3. Keep model/harness routing and cache keepalive advisory until LegionForge has matched-task benchmarks and provider billing data.
4. Treat 90% as Nate's reported target for an experiment, not as an expected result for this project.
5. Treat `/loop 3m` keepalive as a bounded Anthropic experiment, never as an always-on optimization.

## 2026-08-29 release and R&D update

Problem: the project needed a public, attributable release and a current
developer-focused research direction without overstating independent
authorship.

Evidence: `LegionForge/context-governor` was created publicly on GitHub;
`v0.1.0` and `v0.1.1` were published; commit `efaf4c0` added the developer
context-management R&D note; GitHub topics were added for `ai-agents`,
`context-engineering`, `token-optimization`, `codex`, and related terms.

Mechanism: the repository now separates source attribution, transferred
practices, and LegionForge project decisions. The R&D note records current
first-party guidance around repository maps, just-in-time retrieval,
structured state, compaction, and bounded tools, with matched-task validation
required before adopting defaults.

Transfer: public agent-workflow artifacts should identify their source lineage
prominently, preserve exact evidence in a durable register, and treat research
recommendations as hypotheses until quality-adjusted benchmarks pass.

## Uncertainty

The supplied article is partially paywalled, and the public YouTube page did not expose a full transcript. The transcript-derived rules above are therefore confidence-rated as medium until verified against the video or a first-party transcript. Provider billing, cache discounts, cache refresh semantics in Claude Code, and hidden context remain provider-specific; do not infer them from local counters.

## Provenance stamp

AI tool: OpenAI Codex via API  
Provider: OpenAI  
Model ID: not exposed in the session metadata  
AI role: research synthesis and policy drafting  
Human author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org  
Created/revised: 2026-08-28 America/Chicago
