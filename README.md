# Eeshan's Agent Skills

Some minimal agent skills I have been consistenly using for my agentic coding workflows. If you're a uni-tasker like me, then you might find them useful.  

These skills are designed to be small, composable, and work across any coding agent (Claude Code, Codex, Pi, Qwen). My working philosophy is intentionally minimal, uni-tasking, understandable and with a human-in-the-loop perspective, so these few skills and guardrails have been working beautifully if you're the one always wanting to be in control of your work. 

## Quickstart

```bash
npx skills@latest add eeshansrivastava89/skills
```

Pick the skills you want and which coding agents to install them on. 

## What's Included

### Context Management

Skills for saving and restoring session context. Regardless of the model choice (frontier or local), working in small, well-defined sessions produces significantly better output and control in my experience. I use these skills religiously after every constrained working sessions (save context after every ~200K-300K tokens used, clear context, and then restore context in the new session). 

- **[context-save](./skills/context-management/context-save/SKILL.md)** — Captures a compact snapshot of your session state (task, progress, decisions, next actions) and writes it to `.pi/`, `.claude/`, and `.codex/context.md` so any tool can pick up where you left off.
- **[context-restore](./skills/context-management/context-restore/SKILL.md)** — Reads the saved context file, validates it against current git state, surfaces any discrepancies, and gets you back to work.

### Engineering

Day-to-day coding skills.

- **[commit](./skills/engineering/commit/SKILL.md)** — Create a focused git commit with a conventional message. Approval-gated, anti-force-push guardrails built in. 

### Guardrails

Install behavioral guardrails across all your coding agents.

- **[agent-guardrails](./skills/guardrails/agent-guardrails/SKILL.md)** — Writes working philosophy and guardrails to `.agents/AGENTS.md`, `.claude/CLAUDE.md`, and `.codex/AGENTS.md` so any agent you use has the same constraints. Again, this is my intentionally minimal, constrained and human-in-the-loop working philosophy that ensures high quality output from your agentic coding sessions. 

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
