# Eeshan's Agent Skills

Agent skills I use every day for real engineering — not vibe coding.

These skills are designed to be small, composable, and work across any coding agent (Claude Code, Codex, Pi, Qwen). They're based on hard-won experience shipping production apps with AI assistants.

## Quickstart

```bash
npx skills@latest add eeshansrivastava89/skills
```

Pick the skills you want and which coding agents to install them on. That's it.

## What's Included

### Context Management

Skills for saving and restoring session context — so you never lose your train of thought between sessions, regardless of which agent you're using.

- **[context-save](./skills/context-management/context-save/SKILL.md)** — Captures a compact snapshot of your session state (task, progress, decisions, next actions) and writes it to `.pi/`, `.claude/`, and `.codex/context.md` so any tool can pick up where you left off.
- **[context-restore](./skills/context-management/context-restore/SKILL.md)** — Reads the saved context file, validates it against current git state, surfaces any discrepancies, and gets you back to work in seconds.

### Engineering

Day-to-day code work skills.

- **[commit](./skills/engineering/commit/SKILL.md)** — Create a focused git commit with a conventional message. Approval-gated, anti-force-push guardrails built in.

### Guardrails

Install behavioral guardrails across all your coding agents.

- **[agent-guardrails](./skills/guardrails/agent-guardrails/SKILL.md)** — Writes working philosophy and guardrails to `.agents/AGENTS.md`, `.claude/CLAUDE.md`, and `.codex/AGENTS.md` so any agent you use has the same constraints. Merges with existing config — never overwrites.

## Why These Skills Exist

### Context loss is the #1 productivity killer

Every time you close a session, you lose context. When you reopen, the agent starts cold — it doesn't know what you were working on, what decisions you made, or where you stopped. You spend the first 15 minutes re-explaining everything.

**context-save / context-restore** fix this. One command before you close, one command when you reopen. The agent picks up exactly where you left off — across any tool.

### Agents need guardrails, not autonomy

The default agent behavior is to jump straight to code. These guardrails enforce a healthier loop: research first, propose a plan, get approval, then execute in small chunks with verification at every step.

## Philosophy

- **Tool-agnostic** — Skills write to `.pi/`, `.claude/`, and `.codex/` so you're never locked in to one agent
- **Approval-gated** — Destructive operations (commits, force-push) always require explicit sign-off
- **Codebase is truth** — Context files are memory aids, not authority. Always verify against actual state.
- **Small and composable** — Each skill does one thing well. Mix and match with skills from other authors.
- **Explicit invocation** — User-invoked skills only fire when you type the command. No surprise triggers.

## Compatibility

These skills work with:
- Claude Code
- OpenAI Codex
- Pi
- Qwen Code

## License

MIT — do whatever you want. Attribution appreciated but not required.