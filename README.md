# claude-config

My global Claude Code configuration: behavioral guidelines plus a curated set of engineering skills and review-persona agents.

## Contents

- **`CLAUDE.md`** — global behavioral guidelines merging three layers:
  - **Superpowers** ([obra/superpowers](https://github.com/obra/superpowers)) — Clarify → Design → Plan → Code → Verify, enforced on every task, no exceptions.
  - **GSD (Get Shit Done)** — project/task tracking layer, auto-initialized in every project.
  - **Ralph Loop** — optional autonomous execution for well-defined, walk-away tasks.
  - Plus Karpathy-style coding discipline (simplicity, surgical diffs, verifiable goals) and a supplemental skills layer (below).
- **`skills/`** — 6 skills cherry-picked from [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) (MIT license) to fill gaps Superpowers/GSD don't cover: `security-and-hardening`, `performance-optimization`, `observability-and-instrumentation`, `doubt-driven-development`, `api-and-interface-design`, `source-driven-development`.
- **`agents/`** — 2 review personas from the same source: `security-auditor`, `web-performance-auditor`.

## Why not the whole `agent-skills` plugin?

`agent-skills` ships its own meta-skill/router and slash commands. Running it alongside Superpowers means two frameworks competing to route every session — command collisions and conflicting phase sequencing. Instead, only the gap-filling skills are pulled in individually here; they trigger on their own domain-specific conditions (touches auth → `security-and-hardening`, perf concern → `performance-optimization`, etc.) rather than acting as a second router. See `CLAUDE.md` Section 7 for the exact trigger table.

## Install

```bash
cp CLAUDE.md ~/.claude/CLAUDE.md
cp -r skills/* ~/.claude/skills/
cp agents/*.md ~/.claude/agents/
```

Requires [Superpowers](https://github.com/obra/superpowers) and [GSD](https://github.com/get-shit-done-ai) installed separately as Claude Code plugins — this repo only covers the CLAUDE.md wiring and the supplemental skills.

## License

`CLAUDE.md` is original. Files under `skills/` and `agents/` are copied from [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills), MIT licensed.
