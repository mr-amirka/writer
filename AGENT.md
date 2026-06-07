# AI Agent Entry Point

> Entry point for AI agents in the book writing workspace.

## 📖 Getting Started

Read **[CLAUDE.md](CLAUDE.md)** — the main instructions file before performing any task.

## 📋 Working Principles

1. **Read CLAUDE.md before any task**
2. **Three spaces:** USER_DRAFT → AGENT_DRAFT → APPROVED
3. **Do not edit USER_DRAFT** without explicit author permission
4. **Minimum 3 variants** in AGENT_DRAFT
5. **APPROVED — highest priority**

---

## 🛠️ AI Agent Notes: Tool Behavior

*Learned through experience. To avoid relearning every session.*

### create_new_file
- **Does NOT accept absolute paths** — interprets them as relative. Passing /Users/.../AGENT.md creates a Users/ folder inside the project.
- **Solution:** always pass a relative path — AGENT.md, books/ru/mur/README.md, etc.
- To create a file with an absolute path, use run_terminal_command with cat >.

### run_terminal_command
- Shell is **not stateful** — each command runs in a new instance. Do not rely on a previous cd.
- Multi-line commands with && and heredoc (<<) in a single argument **do not work** — they fail with an error.
- **Long commands** (e.g., embedding a Python script with -c) exceed the shell's argument limit and fail with "command too long".
- **Solution:** break into separate calls (rm, then cd && cat). For complex multi-step operations (translating a large file, etc.), create a helper script with create_new_file, execute it with run_terminal_command, then delete the script.
- To change directory and run a command, use: cd /path/ && command on a single line without line breaks.

### read_file
- Absolute paths **work fine.**

### edit_existing_file
- Requires reading the file first — cannot call it otherwise.

### single_find_and_replace
- String matching is literal and whitespace-sensitive. Multi-line strings must match indentation exactly.
- Do NOT wrap old/new strings in extra quotes — pass the raw text directly.
- **Best practice:** match on short unique markers (e.g., "### Section Title") rather than entire large blocks. If a block replacement fails, break it into smaller sequential replacements.
- Works best for section-by-section translation of large files.

### create_new_file (additional note)
- This tool wraps content in an extra layer of escaping. If the content contains special characters (quotes, backticks, backslashes), they can break parsing.
- **Solution:** for content with many special characters, use create_new_file with a minimal Python script, then run it.

### General
- Before creating/editing a file, always verify you are in the correct directory. Use ls to confirm.
- For large file transformations (translation, refactoring): create a temporary Python script via create_new_file, run it with run_terminal_command, then delete it. Do NOT try to embed long content inline.
- If a tool call fails, retry with simpler/shorter input before escalating.

---

*AI agent entry point. Created 2024-06-07. Tool notes added 2024-06-07.*
