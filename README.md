# Awesome-LLM-Token-Usage-Reducer

# Top LLM Token Usage Reducer Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Context Compression, Command Output Filtering & Prompt Efficiency*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **LLM Token Usage Reduction**. These tools reduce the number of tokens sent to and returned from large language models — compressing command outputs, filtering verbose logs, deduplicating context, and shaping output behavior — enabling longer AI coding sessions, lower API costs, and reduced context pollution.

**Examples** include RTK (Rust Token Killer), Caveman, Headroom, Token Savior, Repomix, Code2Prompt, OmniRoute, claude-token-efficient, Graphify, and MindStudio Agent Skills Plugin (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, local compression, and transparent token metering — ideal for AI engineers prioritizing cost control, developers building agent pipelines, and teams hitting context window limits.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[MindStudio Agent Skills Plugin](https://www.mindstudio.ai/product/agent-skills-plugin)**  
  npm package (`@mindstudio-ai/agent`) wrapping 120+ business tool capabilities as typed method calls, with auth, rate limiting, and retries managed. Reduces token waste by eliminating redundant API integration code and context. Free to start at mindstudio.ai [citation:9][citation:18].

## Open-Source GitHub Projects

- **[RTK (Rust Token Killer)](https://github.com/rtk-ai/rtk)**  
  **The leading open-source CLI proxy for reducing LLM token consumption by 60-90%.** Written in Rust with <10ms startup. Sits between your AI assistant and the shell, intercepting and compressing command outputs before they reach the context window. **Zero workflow changes** — install once with hooks and all commands are automatically optimized. Real savings: a developer running 15,720 commands saved **138 million tokens** over several weeks [citation:1]. **Command-level savings**: cargo test (91.8%), git status (80.8%), find (78.3%), grep (49.5%) [citation:1]. Built-in analytics via `rtk gain`. Apache 2.0 licensed, no usage limits, no API keys, no telemetry [citation:1]. Works with Claude Code, Cursor, Gemini CLI, Aider, and any terminal-based AI assistant [citation:1].

- **[Caveman](https://github.com/JuliusBrussee/caveman)**  
  **Viral Claude Code plugin that makes AI speak like a caveman to cut output tokens by ~75%.** Core idea: delete articles, filler words, polite expressions, and hesitant phrases while keeping technical terms and code blocks accurate [citation:12]. Three intensity levels: lite (remove filler), full (default — fragmented sentences, short synonyms), ultra (aggressive abbreviations) [citation:12]. Triggered by "caveman mode", "talk like caveman", or `/caveman`. Open-source, compatible with Claude Code and Codex. Gained **20,000+ GitHub stars in half a day** after Hacker News virality [citation:12].

- **[Headroom](https://www.npmjs.com/package/headroom-ai)**  
  **Open-source LLM context compression library and proxy.** `compress(messages, { model: 'gpt-4o' })` returns compressed messages with `tokensSaved` and `compressionRatio` [citation:13]. Features SmartCrusher (duplicate log removal, redundant code, boilerplate, long-range text), **simulation mode** to preview savings without calling LLM, compression hooks for custom pre/post transforms, and **CCR (Compression, Concatenation, Recovery)** architecture [citation:13]. Framework adapters for Vercel AI SDK, OpenAI SDK, Anthropic SDK, and Google Gemini. Also available as **n8n community node** (`n8n-nodes-headroom-token-optimizer`) with direct optimizer and model middleware nodes [citation:3]. Requires running Headroom proxy (`headroom proxy`).

- **[Token Savior](https://github.com/Mibayy/token-savior)**  
  **MCP server that indexes your codebase by symbol** — functions, classes, imports, call graph — so the model navigates by pointer instead of by `cat`. Measured **97% fewer chars injected across 170+ real sessions** [citation:4]. On 96-task tsbench: **80% reduction in active tokens per task** (17,221 → 3,395) [citation:4]. Layered architecture: symbol-graph navigation + persistent memory engine (SQLite WAL + FTS5 + vector embeddings) + **Bash compactors** (34 command output filters) + **PreToolUse Bash rewriter** that shrinks commands before they run [citation:4]. Profiles from `compact-only` (~0.3 KT manifest) to `full` (68 tools, ~6 KT). Install via `pip install "token-savior-recall[mcp]"` or `uvx token-savior-recall`. Composable with RTK (disable one layer if overlapping) [citation:4].

- **[Repomix](https://github.com/yamadashy/repomix)**  
  **Packs your codebase into a single AI-friendly file with token counting and compression.** `repomix --compress` keeps important structure (imports, exports, classes, functions, interfaces) while removing implementation details [citation:5]. `--include` and `--ignore` narrow scope. `--token-count-tree 1000` identifies heavy files; `--split-output 1mb` handles large repos [citation:5]. Essential for preparing code context for AI analysis without exceeding context windows.

- **[Code2Prompt](https://github.com/mariozechner/code2prompt)**  
  **Converts code projects into AI prompts with token counting and cost estimation.** `--tokens` analyzes token usage; `--price --provider openai --model gpt-4` estimates input/output costs [citation:15]. Helps developers fit code within model context windows and make informed decisions about model usage and cost management [citation:6][citation:15].

- **[OmniRoute (OmniRoot)](https://github.com/DiegoSouza/omniroute)**  
  **Open-source MIT-licensed AI gateway routing across 290+ providers and 500+ models.** When one free tier runs dry, fails over automatically. Compresses bloated inputs, build logs, repeated context, and verbose JSON before they hit the model [citation:7]. Realistic savings: **15-95% range depending on workload**, not a flat 75% — code passes through uncompressed [citation:7]. About **1.54 billion free tokens per month** across deduplicated shared pools [citation:7]. Routing and quota failover are the genuinely useful parts; measure compression on your own traffic [citation:7].

- **[claude-token-efficient](https://github.com/drona23/claude-token-efficient)**  
  **Universal CLAUDE.md template (~15 rules) targeting Claude output behavior** — not input context. Core rules: no sycophantic openers/closers, no em dashes, no unsolicited suggestions, no scope creep, no speculation when uncertain [citation:8]. Three domain profiles: coding, agents, analysis. **Conceptual framing is the real value**: input and output tokens are separate cost axes; most practitioners optimize input only [citation:8]. Claimed ~63% output reduction is **directional indicator only** (5 prompts, no variance controls) [citation:17]. Independent benchmark showed **-17.4% cost-to-green** vs baseline on 3 coding challenges [citation:17]. **Trade-off**: CLAUDE.md consumes input tokens every message — net positive only when output volume is high enough [citation:17].

- **[Graphify](https://pypi.org/project/graphify-leo/)**  
  **Extracts codebase structure into a compact graph for token-efficient queries.** On mixed corpus (Karpathy repos + papers + images, 52 files): **71.5x fewer tokens per query vs reading raw files** [citation:10]. First run builds graph (costs tokens); subsequent queries read compact graph. SHA256 cache means re-runs only process changed files [citation:10]. `--watch` auto-syncs as codebase changes [citation:10].

### Additional Strong Open-Source Options

- **GraphifyCompressor** — Dart class using symbol compression, redundancy removal, and structural shorthand. Typical savings: **30-60% of input tokens** depending on content [citation:19].
- **Serena** — Symbol-graph navigation tool (composes with Token Savior; disable overlap via `TS_MEMORY_DISABLE=1` or run compact-only) [citation:4].
- **codebase-memory** — Persistent code graph (composes with Token Savior; disable via `TS_MEMORY_DISABLE=1`) [citation:4].
- **Ponytail** — Output-side compression (complementary to Token Savior) [citation:4].
- **Caveman (output-side)** — Prose compression (complementary layer) [citation:4].

**Frameworks for building custom systems**: Combine **RTK** for Bash output compression with zero workflow changes, **Token Savior** for symbol-graph navigation and persistent memory, **Headroom** for LLM context compression with simulation and custom hooks, **Repomix** for codebase packing with token counting, and **Graphify** for compact graph-based codebase queries to build a complete self-hosted LLM token reduction stack.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- LLM token reducers must preserve semantic accuracy — **aggressive compression can remove meaningful content or degrade model reasoning** [citation:1]. Benchmark savings on your own workload before standardizing; compression ratios vary significantly by command type and content [citation:7]. Output-shaping tools like claude-token-efficient consume input tokens on every message — net savings only apply at sufficient output volume [citation:17].
- Self-hosted open-source solutions require proper integration testing, metering validation, and monitoring for compression-induced errors.

---

**Made for AI engineers, agent developers, platform teams, and developers building cost-efficient LLM pipelines.**  
Let's make LLM token usage reduction more open, accurate, and developer-friendly.
