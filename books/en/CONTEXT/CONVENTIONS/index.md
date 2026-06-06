# Agent Conventions — English domain

Rules for AI agent behavior when working with books in English.
Read together with `/CLAUDE.md`.
Books and domain context: `books/en/`

---

## Language and Communication

- All responses and texts — **in English**, unless the author explicitly requests otherwise.
- When discussing structure or variants — concise, no filler.
- Don't explain what's obvious from code or file structure.

---

## Text Formatting

### Dialogue
English standard: quotation marks, not em dashes.
```
"Are you sure?" he asked.
"No," she replied. "But there's no other way."
```
Em dash — only for interrupted speech or action beats within a line: "I can't—" she started.
Typographic quotes ("curly") preferred over straight quotes.

### Paragraphs
- Dialogue — always a new paragraph.
- Speaker action — same paragraph as the line, following the closing quote.
- Scene or time change — blank line + `* * *`.

### Numbers in text
Under ten — spelled out. 10 and above — numerals in action scenes, spelled out in meditative passages.

---

## Working with Variants

When creating v1 / v2 / v3 for each chapter:

| Variant | Focus |
|---------|-------|
| v1 | Closest to USER_DRAFT: preserves author's voice and intent, minimal deviation |
| v2 | Structural rewrite: different pace, different point of view or event order |
| v3 | Bold experiment: different tone, unconventional opening, shift to a different register |

Don't make variants superficially different — each must offer a genuine choice.

**Each variant includes three files:** `content.md` + `short.md` + `state-snapshot.md`.
This lets the author compare not just the text, but the world state after each variant.

---

## Chapter Transition Protocol

Required before writing chapter N:
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
- `state-snapshot.md` — current state after the last chapter (location, emotions, artifact status). Filled by the agent after each variant.

---

## Styles and RELEASES

- A style lives in `APPROVED/universe/styles/{name}.md`.
- When building a RELEASE the agent takes `APPROVED/chapters/` and rewrites in the voice of the style.
- Facts and plot do not change — only the delivery.
- Each RELEASE is independent and self-contained.

---

## Space Priority

```
APPROVED  >  USER_DRAFT  >  AGENT_DRAFT
```

When facts conflict between spaces — the higher-priority space wins.
The agent never puts anything into AGENT_DRAFT that contradicts USER_DRAFT or APPROVED.
Contradiction found — recorded in `STATUS.md → Pending decisions`, not fixed unilaterally.

## What the Agent Does NOT Do Without Explicit Instruction

- Does not edit `USER_DRAFT/`.
- Does not move content to `APPROVED/` — only the author does that.
- Does not delete old variants from `AGENT_DRAFT/`.
- Does not invent new characters or world facts outside `APPROVED/universe/`.
- Does not change already approved facts from `APPROVED/universe/`.
- Does not update `APPROVED/universe/` unilaterally — only on explicit author instruction.
- Does not write current character state into `APPROVED/universe/` — only into `state-snapshot.md`.

---

## Chapter Size

**Minimum:** 4,000 words — fewer is a fragment, not a chapter.
**Target range:** 7,000–12,000 words — standard for literary prose.
**Maximum without justification:** 18,000 words. Longer only if the content demands it.

If a chapter comes in shorter than minimum — record the reason in `state-snapshot.md` (section "Warnings").
Consistency matters more than any specific number: deviation from the book's average should not exceed 40%.

Detailed analysis: `CONTEXT/RESEARCH/craft/02_chapter_size.md`

---

## Chapter Numbering

Always three digits with leading zeros: `001`, `002`, `099`, `100`.
This ensures correct alphabetical sorting up to chapter 999.

---

## Status and Concept Files

**`STATUS.md`** — agent work tracker. The agent updates it with every status change for a variant or universe element. Structure: tables with phase columns (USER_DRAFT → AGENT_DRAFT → APPROVED). Not to be confused with PLAN.md (narrative plan, not work tracker).

**`BRIEF.md`** — one-page book document. Includes genre, audience, characters, structure, **and theme, moral, anti-moral, and physical anchors**. Agent reads it before each task for the book.

**`FEEDBACK.md`** — reasons for rejected variants. Agent fills this when the author rejects a variant: what specifically didn't work and why. Prevents repeating the same mistakes.

**Canon lore** — tracked in the `## Canon Lore` section of each `state-snapshot.md`. The agent records new world and character facts first established in the chapter. The author decides what to move to `APPROVED/universe/`.

---

## Research Methodology

For any analysis — market, genre, structural — the agent follows the methodology in `CONTEXT/RESEARCH/craft/03_how_to_research.md`.

**Key rule:** analysis starts with fresh data collection, not the model's training knowledge. Training knowledge is secondary data with a cutoff date. Current market conditions, reader patterns, and genre trends require fresh search.

Minimum 4 slices for a new book project: market, reader, competitive, prose.

---

## Naming and Consistency

The folder name in `RELEASES/` must exactly match the style filename in `APPROVED/universe/styles/`.
- Style `main.md` → folder `RELEASES/main/`
- Style `gothic.md` → folder `RELEASES/gothic/`
- No aliases (`raw`, `default`, `base`).

Contents of `RELEASES/{style}/index.md` — full book text, not links to other files.
