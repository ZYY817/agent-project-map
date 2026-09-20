# yq-map

**Teach your AI agent to keep an accurate map of your codebase.**

yq-map is a single Markdown file — an [Agent Skills](https://github.com/anthropics/skills)-format instruction — that shows an AI coding agent how to build and maintain a lightweight project map: a few `MAP.md` files recording where things live, how they relate, and how reliable each claim is. With it, the agent stops re-exploring the whole repository on every task and goes straight to the code that matters.

[中文版 README](README.zh-CN.md)

## What it does

- **Faster code location.** Each entry carries a searchable anchor — a function name, a route string, a distinctive error message — that lands the agent on the right lines, not just the right file.
- **Accuracy by marking, not by promising.** Every entry is labeled `verified`, `assumed`, `unknown`, or `stale`, with a checked-against date — so unverified information can never masquerade as fact.
- **A built-in self-check.** Are the anchors still findable? Have `verified` entries been invalidated by newer changes? Are the links dead? Suspect entries get downgraded and re-checked instead of trusted blindly.
- **Updates ride along with edits.** Change a file the map records → refresh the affected entries in the same pass. No separate maintenance ritual.
- **Bounded scope.** Map only what the task touches; unmapped areas stay explicitly unmapped. Existing docs are linked, never copied — and flagged when they've gone stale.
- **Zero dependencies.** No server, indexer, database, or runtime. If an agent can list, search, and read files, it can use yq-map — Claude Code, Codex, Cursor, Windsurf, or anything that accepts skill files.

## Why it helps

- **Less wandering, more work.** The agent follows the map to the right files and symbols instead of scanning the tree — its context goes to the code that matters, not to exploration.
- **Fewer wrong turns.** Stale and unchecked information carries visible status, so the agent verifies before trusting instead of confidently following outdated directions.
- **Understanding that persists.** The map survives across sessions and task switches — resume a project days later without paying the exploration cost again.
- **Honest coverage.** Unmapped areas are declared unmapped; the agent says "I don't know" instead of inventing an answer.

## Install

**As a skill** — copy `skill/yq-map/` into your tool's skills directory (e.g. `~/.claude/skills/`, `.agents/skills/`). Drop it in, done.

**As rules** — paste the body of `SKILL.md` into your project's `AGENTS.md` (or `CLAUDE.md`, `.cursorrules`). Works with tools that don't support skills at all.

## Files

```
skill/yq-map/
├── SKILL.md                      English
├── SKILL.zh-CN.md                中文版
└── references/
    ├── MAP.example.md            example map (EN)
    └── MAP.example.zh-CN.md      示例地图（中文）
```

## A note

yq-map is a set of instructions, not a guarantee — the map's accuracy ultimately depends on the capability of the model maintaining it. The status labels make that dependence visible instead of hiding it.

## License

MIT — use it, fork it, ship it in your own tooling.
