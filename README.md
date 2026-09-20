# yq-map

**A project map that admits when it's lying.**

Every AI coding agent does the same wasteful thing: re-explore your repository from scratch, every task, every session. The usual fix is a memory bank or a generated code map — but they share a fatal flaw: **nobody checks whether the map is still true.** Code changes daily; the map doesn't. Six weeks later it confidently points at functions that no longer exist, and your agent follows it straight into a wall.

yq-map is a single Markdown file — an [Agent Skills](https://github.com/anthropics/skills)-format instruction set — that teaches any AI agent to maintain an *honest* project map.

[中文版 README](README.zh-CN.md)

## What makes it different

- **Status labels are mandatory.** Every entry is `verified`, `assumed`, `unknown`, or `stale`, with a checked-against date. A map that can't say "I don't know" will eventually say something wrong — confidently.
- **Anchors, not line numbers.** Each entry carries a searchable anchor — a function name, a route string, a distinctive error message — that lands the agent directly on the right *lines*, not just the right file.
- **Bounded by design.** Map only what the task touches; uncovered areas are declared uncovered. The map never pretends to know the whole repo.
- **Self-check built in.** A defined verification pass: are the anchors still findable? Have `verified` entries been invalidated by newer changes? Are the links dead? Lies get downgraded, not hidden.
- **Updates ride along with edits.** Change a file the map records → fix the affected entries in the same pass. No separate maintenance ritual.

## Zero dependencies

No MCP server, no indexer, no database, no runtime. If an agent can list files, search, and read, it can use yq-map — Claude Code, Codex, Cursor, Windsurf, or anything that accepts skill files. Don't use skills? Paste the rules straight into `AGENTS.md` — same file, second install path.

## Does it actually work?

Blind-tested on a real ~2000-file React project. Agents that had never seen the repo:

- built a task-scoped map that reused existing docs — and **flagged the stale ones**
- located a real rendering fix from a single "constraints" line in the map, without scanning the codebase
- caught a planted dead reference **plus four genuine errors** in the map during self-check
- renamed a core function and updated all four affected map anchors **in the same edit** — no separate maintenance pass

Honest footnote: the rules are only as strong as the agent following them — a lazy model writes a lazier map. That's the `assumed` label applied to ourselves.

## Install

**As a skill** — copy `skill/yq-map/` into your tool's skills directory (e.g. `~/.claude/skills/`, `.agents/skills/`). The agent loads it when a task needs project navigation.

**As rules** — copy the body of `SKILL.md` into your project's `AGENTS.md` (or `CLAUDE.md`, `.cursorrules`). Works with tools that don't support skills at all.

## Files

```
skill/yq-map/
├── SKILL.md                      English
├── SKILL.zh-CN.md                中文版
└── references/
    ├── MAP.example.md            example map (EN)
    └── MAP.example.zh-CN.md      示例地图（中文）
```

## License

MIT — use it, fork it, ship it in your own tooling.
