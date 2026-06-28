# Context Management

Skills for saving and restoring session context across coding agents (Claude Code, Codex, Pi, Qwen).

## User-invoked

Reachable only when you type them (`disable-model-invocation: true`).

- **[context-save](./context-save/SKILL.md)** — Save a compact project context snapshot for later resumption. Writes to `.pi/`, `.claude/`, and `.codex/context.md` so any tool can restore.
- **[context-restore](./context-restore/SKILL.md)** — Restore saved project context. Reads from whichever context file exists and validates against current git state.