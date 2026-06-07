# CLAUDE.md — Book Writing AI Workspace

This is the main entry point for all AI assistants in this project.
**Read this file completely before performing any task.**

Additional rules for Cursor: `.cursorrules`
Additional rules for Copilot: `.github/copilot-instructions.md`

---

## Project Purpose

A structured workspace for collaborative book writing between a human author and AI agents. Supports multiple languages through language domains `books/{iso}/`.

---

## Structure Map

```
books/{iso}/
├── CONTEXT/
│   ├── MEMORY/index.md          # Universal author preferences (all books)
│   ├── CONVENTIONS/index.md     # Agent rules: format, tone, behavior
│   └── RESEARCH/                # Global research (craft, genres)
│
└── {bookName}/
    ├── CLAUDE.md                # Book-specific context (read alongside root)
    ├── BRIEF.md                 # Genre, audience, premise + theme and moral — one page
    ├── PLAN.md                  # Chapter-by-chapter plan + character arcs
    ├── STATUS.md                # Agent work tracker (phases: USER_DRAFT → AGENT_DRAFT → APPROVED)
    ├── MEMORY.md                # Author preferences and feedback for this book
    ├── FEEDBACK.md              # Reasons for variant rejections
    ├── RESEARCH/                # Book-specific research
    │
    ├── USER_DRAFT/              # Human author drafts (raw input)
    │   ├── idea.md              # Raw idea notes
    │   ├── prologue.md
    │   ├── chapters/001.md
    │   └── universe/            # Author world sketches — free form
    │       ├── world.md
    │       ├── lore.md
    │       ├── timeline.md
    │       ├── characters/{name}.md
    │       ├── artifacts/{name}.md
    │       └── styles/main.md, {styleName}.md
    │
    ├── AGENT_DRAFT/             # Agent interpretations (minimum 3 variants)
    │   ├── idea/v1.md, v2.md, v3.md
    │   ├── prologue/v1.md ...
    │   ├── universe/            # Structured world interpretations
    │   │   ├── world/v1.md, v2.md, v3.md
    │   │   ├── lore/v1.md ...
    │   │   ├── timeline/v1.md ...
    │   │   ├── characters/{name}/v1.md, v2.md, v3.md
    │   │   ├── artifacts/{name}/v1.md ...
    │   │   └── styles/{styleName}/v1.md, v2.md, v3.md
    │   └── chapters/{NNN}/v{N}/
    │       ├── content.md        # Full chapter text
    │       ├── short.md          # Brief summary ~500 words (for context)
    │       └── state-snapshot.md # World state AFTER chapter + lore for canon
    │
    ├── APPROVED/                # Approved canon (single source of truth)
    │   ├── idea.md              # Final idea formulation
    │   ├── universe/            # ← STABLE REFERENCE LAYER for the agent
    │   │   ├── world.md         # Approved world structure
    │   │   ├── lore.md          # Approved world rules
    │   │   ├── timeline.md      # Approved chronology
    │   │   ├── characters/{name}.md  # Approved character sheets
    │   │   ├── artifacts/{name}.md
    │   │   └── styles/main.md, {styleName}.md
    │   └── chapters/
    │       ├── 001.md           # Final text
    │       └── 001.short.md     # Final summary
    │
    └── RELEASES/                # Final builds for publication
        ├── main/index.md        # Main style (full text)
        └── {styleName}/
            ├── index.md         # Full book in this style
            └── metadata.md
```

---

## Idea Flow

```
USER_DRAFT/idea.md  →  AGENT_DRAFT/idea/v1,v2,v3  →  APPROVED/idea.md
(raw notes)             (agent interpretations)        (final formulation)
```

Full idea structure is in `BRIEF.md`.

---

## Three Workspaces

### Priority in Conflicts

```
APPROVED  >  USER_DRAFT  >  AGENT_DRAFT
```

If a fact in AGENT_DRAFT contradicts USER_DRAFT or APPROVED — the higher space takes priority.
The agent **never** puts anything in its drafts that contradicts APPROVED or USER_DRAFT.
If a contradiction is found — log it in `STATUS.md` and ask the author for a decision.

---

### USER_DRAFT — Author Drafts
Raw human input: ideas, notes, sketches, chapter drafts.
**Do not edit USER_DRAFT without explicit instruction.** This is the author's personal space.
Read it as source material — interpret it in AGENT_DRAFT. Preserve the author's voice.

### AGENT_DRAFT — Agent Interpretations
The agent always creates **at least 3 variants** (`v1`, `v2`, `v3`) for each chapter or major element.
Variants should offer meaningfully different approaches: pacing, point of view, level of detail, tone.
Do not make variants superficially different — they should genuinely offer a choice.
Drafts must not contradict either APPROVED or USER_DRAFT.

### APPROVED — Approved Canon
Highest priority. Content here has passed author review and is canon.
**When writing new chapters, always read APPROVED, not AGENT_DRAFT.**
Only the author moves content from AGENT_DRAFT to APPROVED.

---

## How the Book Universe Works (APPROVED/universe/)

Universe elements go through the same three phases as chapters:

```
USER_DRAFT/universe/    →    AGENT_DRAFT/universe/    →    APPROVED/universe/
(author sketches)            (interpretations, v1-v3)         (stable canon)
```

**`APPROVED/universe/` — stable reference layer.** Without it, an agent writing chapter 20 would need to read all previous 19 chapters — this does not fit in context.

**What is stored in `APPROVED/universe/` (static — changes rarely):**
- Character biographies and initial traits
- World rules (magic, technology, social structure)
- Narrative styles of the book
- World history before the book begins

**What is NOT stored in `APPROVED/universe/` (dynamic — only in state-snapshot):**
- Current character locations
- Emotional state after recent events
- Status of artifacts that changed during the story

**Sync Protocol (preventing desynchronization):**
1. `APPROVED/universe/` is updated **only by the author** — they move the approved variant from `AGENT_DRAFT/universe/`.
2. The agent updates only upon explicit instruction.
3. The agent logs every update in `STATUS.md`.
4. A contradiction between `APPROVED/universe/` and `APPROVED/chapters/` — do not fix independently, add to "Pending Decisions" in STATUS.md.

**Full context for agent = `APPROVED/universe/` + `state-snapshot` of the last approved chapter.**

---

## State Management Protocol (critical)

The agent cannot hold the entire book in context. Follow this protocol strictly:

### Before writing chapter N:
1. Read `APPROVED/chapters/{N-1}.short.md` — the summary of the previous chapter.
2. Find and read `state-snapshot.md` of the approved variant of chapter N-1.
3. Read `APPROVED/universe/characters/` — approved character sheets.
4. Read `APPROVED/universe/world.md` and `APPROVED/universe/lore.md` — world rules.
5. Read `PLAN.md` — what should happen in this chapter according to the plan.

### After writing a chapter variant:
Fill out `state-snapshot.md` following the template (see `AGENT_DRAFT/chapters/001/v1/state-snapshot.md`).

### Golden Rule:
If a fact is not recorded in APPROVED (including APPROVED/universe/) — it is not canon.
Do not invent facts about characters and the world without an explicit source.

---

## Style System

Styles go through the same three phases: `USER_DRAFT/universe/styles/` → `AGENT_DRAFT/universe/styles/` → `APPROVED/universe/styles/`. Each approved style creates a **separate version of the book** in `RELEASES/{styleName}/`.

Style defines:
- Voice and tone (neutral / romantic / sarcastic / goblin / archaic)
- Vocabulary register and lexicon
- Rhythm and sentence length
- Emphasis (action / emotion / description / humor)
- Transformation examples (neutral phrase → in this style)

**Style does not change the plot or facts — only the way the story is told.**
The same chapter text can exist in multiple styles.

---

## Research Locations

| Path | Scope |
|------|-------|
| `books/{iso}/CONTEXT/RESEARCH/` | Universal craft (all books) |
| `books/{iso}/{bookName}/RESEARCH/` | Book-specific research |

---

## Language Domains

Each `books/{iso}/` is independent. New domain — copy the `_template/` and `CONTEXT/` structure in the target language.

| ISO | Language | Status |
|-----|----------|--------|
| `ru` | Russian | `books/ru/` — active, has book `mur/` |
| `en` | English | `books/en/` — active, has book `bess/` |
| `pt` | Portuguese | `books/pt/` — active, has book `lua/` |

---

## Quick Reference

| Task | Where to Look |
|------|---------------|
| Universal author preferences | `books/{iso}/CONTEXT/MEMORY/index.md` |
| Book-specific author preferences | `{book}/MEMORY.md` |
| Agent behavior rules | `books/{iso}/CONTEXT/CONVENTIONS/index.md` |
| Book concept + theme and moral | `{book}/BRIEF.md` |
| Narrative plan | `{book}/PLAN.md` |
| Work progress / task tracker | `{book}/STATUS.md` |
| Rejected variants and reasons | `{book}/FEEDBACK.md` |
| Chapter facts pending canon | `state-snapshot.md` → "Lore for Canon" section |
| World rules (canon) | `{book}/APPROVED/universe/lore.md` |
| Characters (canon) | `{book}/APPROVED/universe/characters/` |
| Narrative styles (canon) | `{book}/APPROVED/universe/styles/` |
| Author world sketches | `{book}/USER_DRAFT/universe/` |
| State after chapter N | `{book}/APPROVED/chapters/N.short.md` + state-snapshot |
| Approved canon | `{book}/APPROVED/` |
| Book-specific research | `{book}/RESEARCH/` |
