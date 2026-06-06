# Convention: Marker System

---

## CONV-006 · Marker Format
`#CONV-006` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Every point in every file (except RELEASES and equivalent clean-output files) carries a marker:

```
`#CONV-NNN` · {agent-id} · YYYY-MM-DD HH:MM · `{status}`
```

- **ID** — globally unique, sequential. Prefix: `CONV-` universal, `CONV-EN-` / `CONV-RU-` / `CONV-PT-` domain-specific.
- **Agent** — model ID that proposed the point, e.g. `claude-sonnet-4-6`.
- **Timestamp** — to the minute, ISO-8601.
- **Status** — one of: `draft` · `accepted` · `rejected`.

When a point is accepted or rejected, the status field is updated in-place. The original text is **never deleted** — only the status field changes.

---

## CONV-006-A · Question Format
`#CONV-006-A` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

When a decision requires author input, the agent raises a marked question:

```
`?CONV-NNN-Q1` · {agent-id} · YYYY-MM-DD HH:MM

**Question text?**

→ **A:** option A
→ **B:** option B
→ **C:** option C

↳ *Awaiting author*
```

When the author answers, their answer is **appended below** the options — the options are never removed:

```
↳ *Awaiting author*

↳ **Author · YYYY-MM-DD HH:MM:** B — reason
```

---

## CONV-006-B · Scope of Markers
`#CONV-006-B` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

**Files that require markers:** all `.md` files in the repository, except:
- `RELEASES/*/index.md` and similar clean-output files (book text for readers)
- `RELEASES/*/metadata.md`
- `README.md`, `README.ru.md`, `README.pt.md` (public-facing documents)

**Files that always require markers:** CONVENTIONS/, CONTEXT/, STATUS.md, BRIEF.md, PLAN.md, MEMORY.md, FEEDBACK.md, APPROVED/universe/*, state-snapshot.md.

---

## Open Questions

`?CONV-006-Q1` · claude-sonnet-4-6 · 2026-06-06 15:30

**Should markers be applied retroactively to all existing files, or only to files created or significantly edited going forward?**

→ **A:** Retroactive — all existing files get markers in a single pass now (large operation, ~100+ files).
→ **B:** Forward-only — markers apply to new files and files actively edited; existing files are not touched unless they are being changed for another reason.
→ **C:** Hybrid — CONVENTIONS and meta files (STATUS, BRIEF, PLAN, MEMORY, FEEDBACK, state-snapshot, universe) are marked now; chapter text files (USER_DRAFT/chapters/, AGENT_DRAFT/chapters/, APPROVED/chapters/) are marked only as new chapters are added.

↳ *Awaiting author*

↳ **Author · 2026-06-06:** C — apply to CONVENTIONS and meta-files now; chapter files only as new chapters are added.

---

`?CONV-006-Q2` · claude-sonnet-4-6 · 2026-06-06 15:30

**ID namespace: should IDs be globally unique across all domains, or scoped per domain?**

→ **A:** Global — `CONV-001` means the same rule in `books/ru/`, `books/en/`, `books/pt/`. Domain-specific rules get prefix: `CONV-EN-001`.
→ **B:** Domain-scoped — each domain has its own counter starting at 001; cross-domain references use full path notation.

↳ *Awaiting author*

↳ **Author · 2026-06-06:** A — global IDs, one namespace across all domains.
