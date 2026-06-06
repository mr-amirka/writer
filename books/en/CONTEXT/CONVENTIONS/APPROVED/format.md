# Convention: Text Format — English Domain

Migrated from `CONTEXT/CONVENTIONS/index.md` · 2026-06-06 15:30
Status of all points below: `accepted` (in use since 2026-06-05)

---

## CONV-EN-001 · Language
`#CONV-EN-001` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

All responses and texts — **in English**, unless the author explicitly requests otherwise.
When discussing structure or variants — concise, no filler.
Don't explain what's obvious from code or file structure.

---

## CONV-EN-002 · Dialogue Formatting
`#CONV-EN-002` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

English standard: quotation marks, not em dashes.

```
"Are you sure?" he asked.
"No," she replied. "But there's no other way."
```

Em dash — only for interrupted speech or action beats within a line: `"I can't—" she started.`
Typographic quotes ("curly") preferred over straight quotes.

**Paragraphs:**
- Dialogue — always a new paragraph.
- Speaker action — same paragraph as the line, following the closing quote.
- Scene or time change — blank line + `* * *`.

**Numbers:** Under ten — spelled out. 10 and above — numerals in action scenes, spelled out in meditative passages.

---

## CONV-EN-003 · Chapter Size
`#CONV-EN-003` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

**Minimum:** 4,000 words — fewer is a fragment, not a chapter.
**Target range:** 7,000–12,000 words — standard for literary prose.
**Maximum without justification:** 18,000 words. Longer only if the content demands it.

If a chapter comes in shorter than minimum — record the reason in `state-snapshot.md` (section "Warnings").
Consistency matters more than any specific number: deviation from the book's average must not exceed 40%.

Detailed analysis: `CONTEXT/RESEARCH/craft/02_chapter_size.md`
