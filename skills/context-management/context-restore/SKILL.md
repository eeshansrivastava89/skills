---
name: context-restore
description: Restore saved project context for later resumption. Use only when explicitly invoked via $context-restore, /skill:context-restore, or manual selection.
metadata:
  short-description: Rehydrate project context
compatibility: Codex, Claude Code, Pi, Qwen
disable-model-invocation: true
---

# Context Restore

Run this skill only on explicit invocation:
- `$context-restore` in Codex
- `/skill:context-restore` in Pi
- or direct/manual skill selection

Do not trigger implicitly from natural-language phrases.

## Goal

Rebuild working memory from a saved context file, then validate against the current codebase and git state.

Check `.pi/context.md`, `.claude/context.md`, and `.codex/context.md` — all paths are relative to the **current working directory**, not the home directory. Use `./.pi/context.md`, etc. Never write to or read from `~/.pi/context.md`.

## Steps

### 1. Find Context File

Check in this order (all paths relative to the current working directory):
1. `.pi/context.md`
2. `.claude/context.md`
3. `.codex/context.md`

Do **not** look in the home directory (`~/.pi/context.md`, etc.). Context files are always project-local.

If multiple exist, prefer the highest-priority one and note whether the others differ materially.

If none exist:
- state that no saved context was found
- fall back to quick repo restoration using current files and git log/status

### 2. Read Saved Context

Extract:
- Project Anchor
- Git Snapshot
- What We Were Doing
- Decisions
- Open Items
- Resume Plan

### 3. Verify Reality

Run:

```bash
git branch --show-current
git status --short
git log --oneline -5
```

Then compare with saved context:
- branch mismatch
- new commits
- changed working tree
- files no longer matching expectations

### 4. Re-scan Key Docs/Files

Quickly re-open key docs and source files tied to the saved task so the current codebase remains the source of truth.

### 5. Present Restoration Summary

Provide:
- which context file was used
- what project/task we were on
- where we left off
- decisions that still apply
- discrepancies since save
- recommended immediate next action

Then ask a focused continuation choice, for example:
1. Continue from saved next action
2. Review/adjust plan first
3. Start a different task

## Rules

- The codebase is the source of truth; the context file is a memory aid.
- Always call out mismatches explicitly.
- Keep the summary concise and actionable.
- Do not assume old context is still valid without checks.
