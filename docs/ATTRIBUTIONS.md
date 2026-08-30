# Attributions and source register

This project is an adaptation, not an independently originated method. The
portable context governor and Codex skill start from Nate B. Jones's two videos
and the references discussed in them, then document LegionForge's transferred
practices and project decisions. Summaries and adaptations below are not
endorsements by the source authors.

## Videos

1. Nate B. Jones, “Paste This Into Claude: 15 Rules to Never Hit a Token
   Limit Again,” YouTube, published 2026-07-29. The indexed source record is
   [Engineering Signals](https://engineeringsignals.com/item/2026-W31/youtube-natebjones-001.md),
   and the creator channel is [Nate B Jones on YouTube](https://www.youtube.com/@NateBJones).
   Used for the token-reuse evidence and the context-hygiene practices in
   `docs/TOKEN-MANAGEMENT-POLICY.md` and the field note.

2. Nate B. Jones, “Three OpenAI Engineers Shipped A Million Lines. Your
   Ten-Hour Agent Run Starts Here,” YouTube, published 2026-08-12,
   [canonical video](https://www.youtube.com/watch?v=HZLPhPbw3fM). The
   independent indexed summary is [OpenClawDatabase](https://openclawdatabase.com/news/videos/2026-08-12-progressive-context-shaping-long-agent-runs/).
   Used for progressive context shaping, current-state files, and checkpoint
   practices.

## Other references

| Author or organization | Work | Link | Use in this project |
| --- | --- | --- | --- |
| Anthropic | Effective context engineering for AI agents | [article](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Context selection and tool-contract principles |
| Anthropic | Claude Code features overview; MCP documentation | [features](https://code.claude.com/docs/en/features-overview), [MCP](https://code.claude.com/docs/en/mcp) | Extension model and output-limit evidence |
| OpenAI | Unrolling the Codex agent loop; Inside our in-house data agent | [agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/), [data agent](https://openai.com/index/inside-our-in-house-data-agent/) | Compaction and selective retrieval context |
| OpenCode contributors | Compaction documentation | [documentation](https://opencode.ai/v2/docs/compaction/) | Structured checkpoint fields |
| Nous Research | Hermes context compression and context-engine plugin documentation | [compression](https://hermes-agent.nousresearch.com/docs/developer-guide/context-compression-and-caching/), [plugin](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/developer-guide/context-engine-plugin.md) | Lossless recall and provider-native compression |
| Stephen Schoettler | Hermes-LCM | [repository](https://github.com/stephenschoettler/hermes-lcm) | Recoverable raw history |
| Julius Brussee | Caveman honest numbers | [HONEST-NUMBERS.md](https://github.com/JuliusBrussee/caveman/blob/main/docs/HONEST-NUMBERS.md) | Output-compression tradeoff evidence |
| JetBrains | Speak to AI agents like cavemen to save tokens | [benchmark article](https://blog.jetbrains.com/ai/2026/07/speak-to-ai-agents-like-cavemen-tosave-tokens/) | Independent comparison and quality caveat |
| Anthropic | Claude pricing and prompt caching | [pricing documentation](https://docs.anthropic.com/en/docs/about-claude/pricing) | Provider-specific cache evidence |
| OpenAI | Harness engineering; Codex agent loop; Codex-maxxing for long-running work | [harness](https://openai.com/index/harness-engineering/), [agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/), [Codex-maxxing](https://openai.com/index/codex-maxxing-long-running-work/) | Developer context and continuity R&D |
| Anthropic | Effective harnesses for long-running agents | [engineering article](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) | Long-horizon continuity R&D |

The project’s policies, thresholds, and enforcement levels are LegionForge
project decisions informed by these sources, not quotations or claims made by
the listed authors.

## Provenance stamp

AI tool: OpenAI Codex via API  
Provider: OpenAI  
Model ID: not exposed in session metadata  
AI roles: source verification, documentation editing, and release hygiene  
Human author: JP Cruz <jp@legionforge.org>  
Organization: https://legionforge.org  
Created/revised: 2026-08-29 America/Chicago
