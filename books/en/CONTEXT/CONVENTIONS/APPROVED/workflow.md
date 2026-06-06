# Convention: Workflow — English Domain

Migrated from `CONTEXT/CONVENTIONS/index.md` · 2026-06-06 15:30
Status of all points below: `accepted` (in use since 2026-06-05)

---

## CONV-007 · Working with Variants
`#CONV-007` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Create v1 / v2 / v3 for each chapter or major universe element:

| Variant | Focus |
|---------|-------|
| v1 | Closest to USER_DRAFT — preserves author's voice and intent, minimal deviation |
| v2 | Structural rewrite — different pace, point of view, or event order |
| v3 | Bold experiment — different tone, unconventional opening, genre register shift |

Do not make variants superficially different. Each must offer a genuine, meaningful choice.

**Each variant includes three files:** `content.md` + `short.md` + `state-snapshot.md`.

---

## CONV-008 · Chapter Transition Protocol
`#CONV-008` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Required reading before writing chapter N:
1. `APPROVED/chapters/{N-1}.short.md` — what happened
2. `state-snapshot.md` of the approved variant of chapter N-1 — where everyone is
3. `PLAN.md` — what should happen in N
4. `BRIEF.md` — theme, moral, and physical anchors (section "Theme and Moral")
5. `APPROVED/universe/characters/` — current character sheets (static facts)
6. `APPROVED/universe/world.md` + `lore.md` — world rules
7. `MEMORY.md` — author preferences for this book
8. `FEEDBACK.md` — what was rejected before and why

Do not begin a chapter without this context.

**Static vs. dynamic:**
- `APPROVED/universe/` — permanent facts (biographies, world rules, pre-book history). Changes rarely, only on author instruction.
- `state-snapshot.md` — current state after the last chapter (locations, emotions, artifact status). Filled by the agent after each variant.

---

## CONV-009 · Styles and RELEASES
`#CONV-009` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

- A style lives in `APPROVED/universe/styles/{name}.md`.
- When building a RELEASE the agent takes `APPROVED/chapters/` and rewrites in the voice of the style.
- Facts and plot do not change — only the delivery.
- Each RELEASE is independent and self-contained.

---

## CONV-010 · Space Priority
`#CONV-010` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

```
APPROVED  >  USER_DRAFT  >  AGENT_DRAFT
```

When facts conflict between spaces — the higher-priority space wins.
The agent never puts anything into AGENT_DRAFT that contradicts USER_DRAFT or APPROVED.
Contradiction found — recorded in `STATUS.md → Pending decisions`, not fixed unilaterally.

---

## CONV-011 · What the Agent Does NOT Do Without Explicit Instruction
`#CONV-011` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

- Does not edit `USER_DRAFT/`.
- Does not move content to `APPROVED/` — only the author does that.
- Does not delete old variants from `AGENT_DRAFT/`.
- Does not invent new characters or world facts outside `APPROVED/universe/`.
- Does not change already approved facts from `APPROVED/universe/`.
- Does not update `APPROVED/universe/` unilaterally — only on explicit author instruction.
- Does not write current character state into `APPROVED/universe/` — only into `state-snapshot.md`.

---

## CONV-012 · Chapter Numbering
`#CONV-012` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Always three digits with leading zeros: `001`, `002`, `099`, `100`.
Ensures correct alphabetical sorting up to chapter 999.

---

## CONV-013 · Status and Concept Files
`#CONV-013` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

**`STATUS.md`** — agent work tracker. Updated with every status change for a variant or universe element. Structure: tables with phase columns (USER_DRAFT → AGENT_DRAFT → APPROVED). Not to be confused with PLAN.md (narrative plan, not work tracker).

**`BRIEF.md`** — one-page book document. Includes genre, audience, characters, structure, **and theme, moral, anti-moral, and physical anchors**. Agent reads it before each task for the book.

**`FEEDBACK.md`** — reasons for rejected variants. Agent fills this when the author rejects a variant: what specifically didn't work and why. Prevents repeating the same mistakes.

**Canon lore** — tracked in the `## Canon Lore` section of each `state-snapshot.md`. The agent records new world and character facts first established in the chapter. The author decides what to move to `APPROVED/universe/`.

---

## CONV-014 · Research Methodology
`#CONV-014` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

For any analysis — market, genre, structural — the agent follows the methodology in `CONTEXT/RESEARCH/craft/03_how_to_research.md`.

**Key rule:** analysis starts with fresh data collection, not the model's training knowledge. Training knowledge is secondary data with a cutoff date. Current market conditions, reader patterns, and genre trends require fresh search.

Minimum 4 slices for a new book project: market, reader, competitive, prose.

---

## CONV-015 · Naming and Consistency
`#CONV-015` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

The folder name in `RELEASES/` must exactly match the style filename in `APPROVED/universe/styles/`.
- Style `main.md` → folder `RELEASES/main/`
- Style `gothic.md` → folder `RELEASES/gothic/`
- No aliases (`raw`, `default`, `base`).

Contents of `RELEASES/{style}/index.md` — full book text, not links to other files.

---

## CONV-016 · Git Commits
`#CONV-016` · claude-sonnet-4-6 · 2026-06-06 · `accepted`

All commits must be made solely in the owner's name. No agent attribution — no `Co-Authored-By:`, no model IDs, no AI tool signatures of any kind in commit messages or metadata.

The commit history is the author's record, not the agent's.

## CONV-016-A · Commit Message Proposal
`#CONV-016-A` · claude-sonnet-4-6 · 2026-06-06 · `accepted`

Before making any commit, the agent must propose the commit message and wait for the owner's approval. Never commit silently or immediately.

Format of the proposal:
```
Proposed commit message:
> {message}

Commit?
```

Only commit after explicit confirmation. If the owner edits the message — use the edited version verbatim.
