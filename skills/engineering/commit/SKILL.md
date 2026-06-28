---
name: commit
description: Create a git commit with conventional message format
disable-model-invocation: false
---

# Commit Workflow

Create a focused git commit with a conventional message.

## Steps

1. Run `git status` to see all changes
2. Run `git diff --staged` to see staged changes
3. Run `git diff` to see unstaged changes
4. Analyze changes and draft commit message:
   - Summarize what changed (not how)
   - Use imperative mood ("Add feature" not "Added feature")
   - Keep first line under 50 characters
   - Add body if needed for context
5. Show proposed commit message and ask for approval
6. If approved:
   - Stage relevant files (`git add`)
   - Create commit with the message
   - Show result

## Commit Message Format

```
<type>: <short description>

<optional body explaining why, not what>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `refactor`: Code change that neither fixes nor adds
- `docs`: Documentation only
- `test`: Adding or fixing tests
- `chore`: Maintenance, dependencies, config

## Rules

- Never commit without explicit user approval
- Never use `--force` or destructive operations
- Don't commit secrets, credentials, or .env files
- Keep commits focused (one logical change)
