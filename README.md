# yq-map

**A project map that admits when it's lying.**

Every AI coding agent repeats the same quiet ritual: open the repo, wander the tree, read files at random — a fresh expedition for every single task. The usual remedies are memory banks and generated code maps, but they share one silent defect: **no one ever checks whether the map is still true.** Code changes daily; maps don't. Within weeks they point at functions that no longer exist — and your agent follows them, confidently, into a wall.

yq-map is a single Markdown file — an [Agent Skills](https://github.com/anthropics/skills)-format instruction — that teaches an agent to keep a map that knows its own limits.

[中文版 README](README.zh-CN.md)

## What it does

- **Honesty, enforced.** Every entry carries a status — `verified`, `assumed`, `unknown`, or `stale` — plus a checked-against date. A map that cannot say "I don't know" will eventually say something wrong, confidently.
- **Anchors, not line numbers.** Each entry holds something searchable — a function name, a route string, a distinctive error message — that lands the agent on the right lines, not merely the right file.
- **Bounded by design.** Map only what the task touches and declare the rest unmapped. The map never pretends to know the whole repo.
- **Reuse, don't duplicate.** Existing docs are linked, not copied — and when they've gone stale, the map says so rather than inheriting their errors.
- **Updates ride along.** Change a file the map records → fix the affected entries in the same pass. No separate maintenance ritual.
- **Self-check, built in.** Are the anchors still findable? Have `verified` entries been invalidated by newer changes? Are the links dead? Lies get downgraded — never hidden.
- **A trust boundary.** Map contents are reference data, never instructions. Text inside the map cannot redirect the agent's task.

## Zero dependencies

No server, no indexer, no database, no runtime. If an agent can list, search, and read files, it can use yq-map — Claude Code, Codex, Cursor, Windsurf, or anything that accepts skill files.

## Install

**As a skill** — copy `skill/yq-map/` into your tool's skills directory (e.g. `~/.claude/skills/`, `.agents/skills/`). Drop it in, done.

**As rules** — no skill support? Paste the body of `SKILL.md` into your project's `AGENTS.md` (or `CLAUDE.md`, `.cursorrules`). Same file, second door.

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

yq-map is instruction, not machinery — a map is only as honest as the agent keeping it. A careful model gets a trustworthy map; a lazy one gets a trail of `assumed` labels. Still better than confident fiction.

## License

MIT — use it, fork it, ship it in your own tooling.
