---
name: agent-guardrails
description: Install global guardrails and working philosophy to all agent config directories. Use only when explicitly invoked via $agent-guardrails, /skill:agent-guardrails, or manual selection.
metadata:
  short-description: Install guardrails across all agents
compatibility: Codex, Claude Code, Pi, Qwen
disable-model-invocation: true
---

# Agent Guardrails

Run this skill only on explicit invocation:
- `$agent-guardrails` in Codex
- `/skill:agent-guardrails` in Pi
- or direct/manual skill selection

Do not trigger implicitly from natural-language phrases.

## Goal

Write guardrails and working philosophy to **all three** agent config directories so any agent you use has the same behavioral constraints. All paths are relative to the **current working directory**, not the home directory:

1. `.agents/AGENTS.md` (agent-agnostic)
2. `.claude/CLAUDE.md` (Claude Code)
3. `.codex/AGENTS.md` (Codex)

Always write all three. Create directories if they don't exist. Do **not** write to `~/.agents/` or any home-directory path.

Run in your project root for project-local guardrails, or in `~` for global guardrails.

## Steps

### 1. Check Existing Config

Read each config file if it exists. Preserve any existing user content — only append or merge the guardrails section, never overwrite custom instructions.

```bash
ls -la .agents/AGENTS.md .claude/CLAUDE.md .codex/AGENTS.md 2>/dev/null
```

### 2. Write Guardrails

Write the guardrails content below to all three paths (relative to current working directory):
- `.agents/AGENTS.md`
- `.claude/CLAUDE.md`
- `.codex/AGENTS.md`

Create parent directories (`mkdir -p`) if they don't exist.

If a file already has content, append the guardrails section below the existing content with a clear separator (`---`). Do not duplicate the guardrails section if it already exists.

### 3. Guardrails Content

```markdown
## Guardrails

- **NEVER modify this file without approval** — Read-only for the agent
- **NEVER make irreversible changes without approval**
- **NEVER commit unless explicitly asked**

## Working Philosophy

- **Research before code** — Explore codebase and docs first
- **Propose, don't execute** — Present plan, wait for approval
- **Chunk-based delivery** — Complete small pieces, checkpoint
- **Fix root causes** — No workarounds unless stuck
- **Say it when the architecture is tangled** — Don't quietly ship into a mess
- **Concrete plans before big changes** — Target structure, what gets deleted, migration sequence

## Code Principles

- **Readability over cleverness** — Every concept gets one obvious home
- **KISS first** — No layers, registries, or abstractions unless they clearly reduce complexity
- **Human co-ownership is required** — If only the AI can navigate the code, the architecture is wrong
- **Delete dead code aggressively** — No compatibility shims for things nothing uses
- **Glass-box, not black-box** — Memory, reasoning, prompts, diagnostics all visible

## Architecture Principles

- **One source of truth per kind of state** — Never let stores silently compete
- **Separate deterministic logic from LLM logic** — Code owns routing/scheduling/gates; LLM owns synthesis/interpretation
- **One obvious entry point per feature** — If you can't quickly answer "where does this live?", reorganize
- **Preserve what's differentiated** — Don't simplify by flattening the product into something generic

## Verification

- Run tests after code changes
- For UI changes, take screenshots and compare
- If you can't verify it, don't ship it

## Session Flow

- Use `/context-restore` at session start
- Use `/context-save` before ending session
- Use `/commit` when ready to commit (requires approval)
```

### 4. Confirm Back

Return a short confirmation including:
- all file paths written
- whether each was created fresh or merged with existing content
- reminder that guardrails are now active for all agents in this directory

## Rules

- **Always write all three files** — `.agents/AGENTS.md`, `.claude/CLAUDE.md`, `.codex/AGENTS.md`.
- **Never overwrite existing content** — Merge or append only.
- **Idempotent** — Running twice should not duplicate the guardrails section.
- **Project-local by default** — Paths are relative to the current working directory.