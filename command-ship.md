---
description: Prepare a commit and PR body for the current change, stop before pushing
allowed-tools: Read, Grep, Bash(git status), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git log:*)
---

Package the current work. Do not push.

1. `git status` and `git diff` — confirm everything staged belongs to the task, nothing else.
2. Run the test command from `CLAUDE.md`. If it fails, stop and report; do not "fix" it silently.
3. Add only the files that belong: `git add <paths>` (never `git add -A`).
4. Commit. Subject: imperative, ≤ 72 chars, no trailing period. Body only if the *why* is
   not obvious from the subject; wrap at 72.
5. Print the PR body in markdown, nothing else:

```
## What
one paragraph

## Why
one paragraph

## How verified
- exact command run and result

## Risk / undone
- anything unverified, out of scope, or needing a follow-up
```

6. Show `git log --oneline -1` as confirmation and stop.
