# Convention: Task Completeness — English Domain

Approved from `AGENT_DRAFT/completeness.md` · 2026-06-06 15:45
Author approved A–E in conversation · 2026-06-06

---

## CONV-001 · Task Completion Checklist
`#CONV-001` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Before declaring any task done, the agent must verify:

1. **All planned files created.** If a task involves creating N files, confirm N files exist before finishing.
2. **Cross-references updated.** Any file that mentions the created structure (CLAUDE.md, README files, STATUS.md, MEMORY.md, root CLAUDE.md language domain table) — updated.
3. **Explicit remainder declared.** If anything was intentionally left out, state it by name. Never stop silently mid-task.

Prohibited: ending a response with "done" when the file list is incomplete.

---

## CONV-002 · Scope Declaration
`#CONV-002` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

For any task creating or modifying more than 5 files: before starting, declare the scope explicitly:

> "I will create X files in Y folders: [list]. Proceeding."

This makes the task auditable. The author can catch scope misunderstandings before execution, not after.

---

## CONV-003 · Structural Parity Check
`#CONV-003` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

When duplicating a structure to another domain or creating an "equivalent" of an existing structure:

1. Count files in the reference (`find {reference} -type f | wc -l`).
2. Count files in the new structure.
3. Declare the comparison explicitly.
4. If there is a difference — state which files are missing and whether the gap is intentional.

Example: "mur/ has 53 files. bess/ has 41. Missing: chapter 002, alternate style. This is intentional for a first-pass demo."

---

## CONV-004 · Definition of a Complete Demo Book
`#CONV-004` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

A demo book is considered **complete at minimum** when it contains:

| Layer | Required files |
|-------|---------------|
| Root | `CLAUDE.md`, `BRIEF.md`, `PLAN.md`, `STATUS.md`, `MEMORY.md`, `FEEDBACK.md` |
| USER_DRAFT | `idea.md`, `chapters/001.md`, `universe/world.md`, `universe/lore.md`, `universe/characters/{protagonist}.md`, `universe/characters/{deceased-owner}.md`, `universe/characters/{newcomer}.md`, `universe/styles/main.md` |
| AGENT_DRAFT | `universe/world/v1.md`, `universe/world/v2.md`, `universe/characters/{protagonist}/v1.md`, `universe/characters/{protagonist}/v2.md`, `universe/characters/{newcomer}/v1.md`, `universe/styles/main/v1.md`, `chapters/001/v1/content.md`, `chapters/001/v1/short.md`, `chapters/001/v1/state-snapshot.md`, same for v2 and v3 |
| APPROVED | `idea.md`, `universe/world.md`, `universe/lore.md`, `universe/timeline.md`, `universe/characters/{protagonist}.md`, `universe/characters/{deceased-owner}.md`, `universe/characters/{newcomer}.md`, `universe/styles/main.md`, `chapters/001.md`, `chapters/001.short.md` |
| RELEASES | `main/index.md` |

A demo book is considered **fully illustrated** (showing the continuity system) only when it also has chapter 002 with variants.

---

## CONV-005 · STATUS Update on Interruption
`#CONV-005` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

If a multi-step task is interrupted (context limit, session end, user redirect) before completion:

1. Update `STATUS.md` of any affected book to mark what was done and what was not.
2. In the response to the user, explicitly state: "Task partially complete. Done: [list]. Remaining: [list]."
3. Never leave STATUS.md in a state that implies completion when the task is unfinished.
