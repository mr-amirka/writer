# Book Writing AI Workspace

A structured workspace for collaborative book writing between a human author and AI agents. Supports multiple languages through independent language domains (`books/{iso}/`).

Other languages: [Русский](README.ru.md) · [Português](README.pt.md)

---

## What This Is

This framework gives you and an AI agent a shared, organised space for writing a book — with clear rules about who owns what, how drafts move toward canon, and how the agent keeps context across chapters without reading the whole manuscript every time.

**Core idea:** Three spaces with strict priority.

```
USER_DRAFT  →  AGENT_DRAFT  →  APPROVED
(your raw input)  (agent interprets)  (approved canon)
```

The agent never changes your raw drafts. You never manually write the agent's interpretations. Only you promote content to APPROVED.

---

## Repository Structure

```
books/
├── ru/                        # Russian language domain
│   ├── CONTEXT/
│   │   ├── CONVENTIONS/       # Agent behaviour rules for this language
│   │   ├── MEMORY/            # Universal author preferences (all books)
│   │   └── RESEARCH/          # Craft research (structure, chapter size, genres...)
│   ├── _template/             # Copy this to start a new book
│   └── {bookName}/            # A specific book
│
├── en/                        # English language domain
│   ├── CONTEXT/
│   ├── _template/
│   └── {bookName}/
│
└── pt/                        # Portuguese language domain
    ├── CONTEXT/
    ├── _template/
    └── {bookName}/
```

Each language domain is independent. The `_template/` folder is your blank book starter.

---

## Quick Start

### 1. Create a new book

Copy the template for your language:
```
books/en/_template/  →  books/en/my-book/
```

### 2. Fill in the concept files

Start with these files in your new book folder — write freely, no required format:

| File | What to put there |
|------|------------------|
| `USER_DRAFT/idea.md` | Your raw concept — stream of consciousness, images, questions |
| `BRIEF.md` | Genre, audience, premise, theme (one page max) |
| `PLAN.md` | Chapter-by-chapter outline and character arcs |
| `USER_DRAFT/universe/world.md` | What kind of world this is |
| `USER_DRAFT/universe/characters/{name}.md` | Each character — who they are, what they want |

### 3. Ask the agent for interpretations

Point the agent to your book's `CLAUDE.md` and ask it to interpret one element at a time. For example:
- "Interpret `USER_DRAFT/idea.md` into three variants"
- "Write three versions of chapter 001 based on my draft"

The agent always creates **minimum 3 variants** (v1, v2, v3). Each variant is a meaningfully different approach, not a cosmetic variation.

### 4. Review and approve

Read the variants. When you're ready:
- Tell the agent which variant you prefer (or what to combine)
- Move the chosen content to `APPROVED/` yourself — the agent never does this unilaterally

### 5. Continue writing

For each new chapter, the agent reads:
1. The summary of the previous approved chapter (`APPROVED/chapters/N.short.md`)
2. The state snapshot from the last chapter (`state-snapshot.md`)
3. The approved universe facts (`APPROVED/universe/`)
4. The narrative plan (`PLAN.md`)

This is how the agent maintains context without re-reading the entire manuscript.

---

## The Three Spaces

### USER_DRAFT — your raw input
Everything you write goes here first. The agent reads it but **never edits it**. Write however you like: fragments, contradictions, questions to yourself. The agent will interpret, not fix.

### AGENT_DRAFT — agent interpretations
The agent creates minimum 3 variants for each chapter or universe element. Each variant folder contains:
- `content.md` — full text
- `short.md` — ~500-word summary for context reuse
- `state-snapshot.md` — world state after this chapter (characters' locations, emotions, active threads)

Variants must offer **real choices** — different pace, PoV, tone — not minor wording differences.

### APPROVED — your canon
The highest priority. Only you move content here. Once something is APPROVED, the agent treats it as immutable fact. When writing any new chapter, the agent reads APPROVED and ignores AGENT_DRAFT.

**Priority rule:** `APPROVED > USER_DRAFT > AGENT_DRAFT`

If the agent finds a contradiction between spaces — it records it in `STATUS.md` and waits for your decision. It never resolves contradictions unilaterally.

---

## State Management

A novel is too long to fit in context. The framework solves this with two layers:

**Static layer — `APPROVED/universe/`**
Permanent facts that rarely change: character biographies, world rules, history before the book begins.

**Dynamic layer — `state-snapshot.md`**
The world state *after* each chapter: where each character is, what they feel, what's changed, what narrative threads are open. The agent fills this after every variant.

Before writing chapter N, the agent reads:
- `APPROVED/chapters/{N-1}.short.md` — what happened
- `state-snapshot.md` of chapter N-1 — current state
- `APPROVED/universe/` — the permanent facts

This is enough to write consistently without re-reading everything.

---

## Tracking Work

**`STATUS.md`** — the agent's work log. Updated after every action. Contains:
- Current task
- Phase of each chapter and universe element (USER_DRAFT / AGENT_DRAFT / APPROVED)
- Questions waiting for your decision

**`FEEDBACK.md`** — rejected variants log. When you reject a variant, the agent records what didn't work and why. Prevents the same mistakes from repeating.

**`MEMORY.md`** — your preferences for this specific book (tone references, what to avoid, what you've approved).

---

## Styles and Multiple Releases

A book can be released in multiple narrative styles — same plot and facts, different voice and tone.

Styles live in `APPROVED/universe/styles/`. Each approved style generates a separate `RELEASES/{styleName}/` folder with the full text of the book rewritten in that voice.

Example styles: `main` (default), `romantic`, `gothic`, `sardonic`.

**Style changes delivery, not content.** The agent never changes plot, characters, or facts when applying a style.

---

## Language Domains

Each `books/{iso}/` is independent. Adding a new language means creating a new domain with its own `CONTEXT/` (conventions and research in that language) and its own `_template/`.

Available domains:
- `books/ru/` — Russian (active, includes demo book `mur/`)
- `books/en/` — English (template ready)
- `books/pt/` — Portuguese (template ready)

---

## Agent Entry Points

The agent reads two CLAUDE.md files at the start of any session:

1. **`/CLAUDE.md`** (root) — global architecture, priority rules, state management protocol
2. **`books/{iso}/{book}/CLAUDE.md`** — this specific book's context, special rules, quick links

Before writing a chapter, the agent also reads BRIEF.md, PLAN.md, MEMORY.md, and FEEDBACK.md for the book.

---

## File Reference

| Need to... | Look at |
|-----------|---------|
| Start a new book | `books/{iso}/_template/` |
| Check agent behaviour rules | `books/{iso}/CONTEXT/CONVENTIONS/index.md` |
| Track work progress | `{book}/STATUS.md` |
| See the narrative plan | `{book}/PLAN.md` |
| Read the concept + theme | `{book}/BRIEF.md` |
| Find approved character facts | `{book}/APPROVED/universe/characters/` |
| Find approved world rules | `{book}/APPROVED/universe/lore.md` |
| See current state after last chapter | Last approved chapter's `state-snapshot.md` |
| Record why a variant was rejected | `{book}/FEEDBACK.md` |
| Read craft research | `books/{iso}/CONTEXT/RESEARCH/` |
