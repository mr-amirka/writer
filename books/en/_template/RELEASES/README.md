# RELEASES — Final Builds

Assembled versions of the book for publication or distribution. Each folder is a separate narrative style.

**The agent assembles a RELEASE on the author's request, taking `APPROVED/chapters/` and applying the style from `APPROVED/universe/styles/`.**

---

## Structure

```
RELEASES/
├── main/                  # Main style (styles/main.md) — full text
│   └── index.md
├── romantic/              # Style: styles/romantic.md
│   ├── index.md           # Full book text in this style
│   └── metadata.md        # What changed relative to main
├── gothic/                # Style: styles/gothic.md
│   ├── index.md
│   └── metadata.md
└── {styleName}/           # Any other style
    ├── index.md
    └── metadata.md
```

**Naming principle:** the folder is named the same as the style file in `APPROVED/universe/styles/`. No `raw`, `default`, or other aliases.

**Contents of index.md:** full book text, not links. The reader must see the final result without opening other files.

---

## RELEASE Assembly Process

1. Verify that all needed chapters are in `APPROVED/`.
2. Load the style from `APPROVED/universe/styles/{styleName}.md`.
3. For each approved chapter: rewrite in the style's voice, preserving facts and plot.
4. Assemble: prologue + chapters in order + epilogue → `RELEASES/{styleName}/index.md`.
5. Fill in `metadata.md`.

**Style does not change plot, characters, or facts — only the delivery.**
