# CLAUDE.md — Global Behavioral Guidelines
# Merges: Karpathy Principles + Superpowers Workflow + GSD Task Management
# Place in ~/.claude/CLAUDE.md for global use across all projects
# Override or extend with a project-level CLAUDE.md in each repo

---

## SECTION 1: Karpathy Principles
### (Core LLM coding discipline — applies to everything)

### 1. Think Before Coding
**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### 2. Simplicity First
**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- If you write 200 lines and it could be 50, rewrite it.
- Ask: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### 3. Surgical Changes
**Touch only what you must. Clean up only your own mess.**

- Don't improve adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.
- Every changed line should trace directly to the user's request.

### 4. Goal-Driven Execution
**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Add feature X" → "Write tests for X, then make them pass"

For multi-step tasks, state a brief plan before starting:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently.
Weak criteria ("make it work") require constant clarification.

---

## SECTION 2: Superpowers Workflow
### (When and how to use structured development methodology)

Superpowers is active globally, for every project, on every task. Applied without exception.

**When Superpowers applies:** everything — new features, bug fixes, refactors, one-liners, all of it. There is no "too trivial" carve-out. Deciding a task is trivial enough to skip the gate is a subjective judgment call, and subjective judgment calls are what produce inconsistent behavior across sessions. Don't make that call.

**The only legitimate skip** is an explicit, in-the-moment instruction from the user ("skip planning for this one," "just make the change"). That's their decision to make, not an inference for me to draw.

**Phase sequence (enforce this order):**
1. **Clarify** — ask questions before writing any code
2. **Design** — propose architecture/approach, wait for sign-off
3. **Plan** — break into micro-tasks (2–5 min each) with file paths and verify steps
4. **Code** — implement test-first (TDD red → green → refactor)
5. **Verify** — confirm all tests pass, review against the plan

For genuinely mechanical work (renames, copy/paste, single-line fixes with obvious scope), still run the phases — they just resolve fast: Clarify and Design collapse to a one-line restatement of what you're about to do, Plan is a single step. Compressing the phases is fine; skipping them is not.

**Never skip to Code without completing Clarify → Design → Plan, unless the user explicitly said so in that moment.**

**Slash commands available:**
- `/brainstorming` — explore requirements before any design
- `/execute-plan` — run batched implementation with review checkpoints
- `/using-superpowers` — remind Claude that Superpowers is active this session

---

## SECTION 3: GSD Task Management
### (How to use Get Shit Done alongside Superpowers)

**GSD is the project management layer. Superpowers is the engineering layer. They don't overlap.**

| Superpowers does... | GSD does... |
|---|---|
| Clarify → Design → Plan → Code → Verify | Track what tasks exist and their status |
| Enforce TDD and code review | Surface what's next at session start |
| Structured debugging methodology | Record what was completed |
| Token-efficient planning via markdown | Maintain continuity between sessions |

**Session Start Protocol (always do this first, in every project):**
1. Check for a `.planning/` directory. **If it doesn't exist, initialize GSD for this project before doing anything else** — do not silently work outside GSD just because it hasn't been set up yet. This applies even to small or throwaway-looking projects; consistency means every project gets tracked, not just the ones that happen to have `.planning/` already.
2. Check GSD for open tasks on this project
3. Report: what's in progress, what's blocked, what's next
4. Then ask the user if they want to continue a task or start something new
5. Never assume — surface the options

**Sizing work within GSD, not skipping it:** GSD has its own lightweight paths (`gsd-fast`, `gsd-quick`) for small or mechanical tasks — use those instead of deciding a task is too small for GSD entirely. The task still gets tracked and committed; it just skips optional ceremony GSD itself defines, rather than ceremony I decide to skip.

**When to create GSD tasks:**
- After Superpowers writing-plans completes → create a GSD task per milestone
- When a bug is identified but not immediately fixed → log it in GSD
- When user mentions something to do later → capture it in GSD immediately

**When to update GSD:**
- Mark a task done before moving to the next one
- If a task is blocked, update its status with the reason
- At end of session, confirm GSD reflects actual current state

**Never lose track of where we left off.** GSD is the source of truth between sessions.

---

## SECTION 4: Tool Priority Rules
### (Which tool to reach for and when)

```
New feature request
  └─→ Superpowers: clarify → design → plan
        └─→ GSD: create tasks from plan
              └─→ Superpowers: code + verify each task
                    └─→ GSD: mark tasks complete

Bug report
  └─→ GSD: log the bug if not fixing now
  └─→ Superpowers: systematic-debugging (4-phase)
        └─→ GSD: mark resolved when verified

Session start
  └─→ GSD: initialize if missing, then check open tasks
        └─→ Report status, ask user what to work on
              └─→ Superpowers: activate for whatever task is chosen — every time, no exceptions
```

---

## SECTION 5: Project-Level Overrides
### (Add these in each project's local CLAUDE.md)

Each project repo should have its own CLAUDE.md that adds:
- Stack and architecture overview
- Key conventions (naming, file structure, testing approach)
- Open known issues / bugs
- Priority order for current sprint

Project-level files add context, not exceptions — they must not redefine which Superpowers/GSD phases apply. The zero-exception policy in Sections 2–3 is global and does not vary by project; that's what makes it consistent.

Example project CLAUDE.md additions:
```markdown
## Project: Salat Nudge
Stack: Flutter / Dart, Android-first (iOS to follow)
LLC: Battuta Labs LLC
Open issues: Jumu'ah nudge bug, Arabic font readability, points calc
Priority: Fix nudge timing logic first, then Jumu'ah, then UI polish
Testing: Widget tests required for all prayer time logic
```

---

**These guidelines are working if:**
- Claude asks clarifying questions before writing code
- GSD is initialized and checked at every session start without prompting — in every project, not just the ones already set up
- No task skips Superpowers phases without an explicit, in-the-moment user instruction
- Diffs are small and surgical
- Tasks don't get lost between sessions
- Plans are written before implementation, not after mistakes
- Behavior is the same from one project to the next — you never have to remember which projects use GSD/Superpowers and which don't

---

## SECTION 6: Ralph Loop — Autonomous Execution
### (When to use iterative self-correcting loops)

Ralph Loop intercepts Claude's exit and re-feeds the same prompt until completion criteria are met. Use it for well-defined tasks you can walk away from.

**When to use Ralph Loop:**
- Tasks with clear, verifiable completion criteria (tests pass, build succeeds)
- Greenfield features where no human judgment is needed mid-flight
- Bug fixes where the fix is "make the tests green"
- Any task where you want Claude working autonomously while you're away

**When NOT to use Ralph Loop:**
- Tasks requiring design decisions or your approval mid-way
- Unclear requirements (clarify with Superpowers first, THEN ralph)
- Production debugging requiring human judgment
- One-shot tasks — overkill, just run them normally

**The correct sequence with your full stack:**
```
1. GSD        → identify the task
2. Superpowers → clarify → design → plan (with your approval)
3. Ralph Loop  → execute the approved plan autonomously
4. GSD        → mark complete when ralph finishes
5. /revise-claude-md → capture learnings
```

**Command syntax:**
```bash
/ralph-loop "<task with clear completion criteria>" --completion-promise "DONE" --max-iterations 20
```

**Always set --max-iterations as a safety net.**

**Good ralph-loop prompt structure:**
```
Implement [feature] following the approved plan in plans/.

Requirements:
- [specific requirement 1]
- [specific requirement 2]
- All tests passing

If blocked after 10 iterations, document what's blocking and stop.
Output <promise>COMPLETE</promise> when done.
```

**Windows:** hooks.json already configured to use Git Bash at
"C:/Program Files/Git/bin/bash.exe" — do not revert this setting.

---

## SECTION 7: Supplemental Engineering Skills
### (Cherry-picked from addyosmani/agent-skills — gap-fillers, not a competing router)

Six skills (`~/.claude/skills/`) and two review personas (`~/.claude/agents/`) pulled in from the `agent-skills` project because they cover ground Superpowers + GSD don't. Invoke them automatically, the same way Superpowers and GSD are invoked without being asked:

| Trigger | Skill |
|---|---|
| Touches user input, auth, sessions, storage, or third-party/external integrations | `security-and-hardening` (pair with the `security-auditor` persona for a dedicated pass) |
| Performance requirements exist, or a regression/slowness is suspected | `performance-optimization` (pair with the `web-performance-auditor` persona) |
| Shipping anything that runs in production, or adding logs/metrics/alerts | `observability-and-instrumentation` |
| Designing a REST/GraphQL endpoint, module boundary, or public interface/type contract | `api-and-interface-design` |
| Implementing against a specific framework/library where correctness depends on current docs | `source-driven-development` |
| About to commit a non-trivial or irreversible decision, or working in unfamiliar code | `doubt-driven-development` (spawns a fresh-context adversarial reviewer from the main session only — never from inside a persona/subagent) |

**Never install the `agent-skills` plugin/marketplace itself or its `using-agent-skills` meta-skill.** It duplicates Superpowers' job as session router — running both as active routers causes them to fight over phase sequencing and command names. Cherry-picked skills only.

---

## SECTION 8: Local Doc Preview (design docs, specs, plans)
### (Automatic local HTTP preview for specs and plans — no need to ask)

Every design doc, spec, or plan written or edited anywhere under `docs/superpowers/specs/**/*.md`, `docs/superpowers/plans/**/*.md`, or `.planning/**/*.md`, in any project, is automatically served on a local HTTP preview — no need to ask for it.

**Mechanism:** a global `PostToolUse` hook (matcher `Write|Edit`) in `~/.claude/settings.json` calls `~/.claude/tools/doc-viewer/hook.py` on every matching file write/edit. This is enforced by the hook, not by this file — CLAUDE.md text alone cannot trigger automated actions; only settings.json hooks execute on events. This section documents the behavior for visibility.

- One persistent, idempotent server per project (`~/.claude/tools/doc-viewer/index_server.py`), tracked in `~/.claude/tools/doc-viewer/registry.json` (project root → port). Re-scans the directory and re-reads file content on every browser refresh — no restart needed as docs are added or edited.
- The server lists all matching docs in a sidebar (grouped by top-level folder, most-recently-modified first) and renders the selected one as GitHub-flavored markdown.
- The hook surfaces the URL back into context after each matching Write/Edit (`hookSpecificOutput.additionalContext` + `systemMessage`) — relay it to the user rather than re-deriving or re-announcing the feature.
- Binds to `127.0.0.1` only (not exposed on the network). Servers persist across sessions until the machine restarts or the process is stopped manually.
