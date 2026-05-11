---
description: Review the working diff for correctness, edge cases and risk
allowed-tools: Read, Grep, Bash(git diff:*), Bash(git status)
---

Review the current uncommitted work. Do not change code unless a finding needs a one-line fix
to be demonstrable.

1. `git status` and `git diff` — read the whole diff before commenting.
2. For each hunk, open the surrounding function. Judge the change in context, not alone.
3. Look for, in this order:
   - wrong behaviour on empty / None / single-item input
   - error paths that swallow or mislabel failures
   - state mutated that a caller also holds
   - resource leaks (files, sockets, locks, connections)
   - missing or weakened tests for the new behaviour
   - API/CLI/config changes that break existing callers
4. Check the diff for anything unrelated to the stated task.
5. Run the test command from `CLAUDE.md`.

Output, most severe first:

```
SEVERITY  file:line   problem               what to do
```

Then one line: ship it, or fix first with reasons. If the diff is fine, say so plainly — do
not invent findings.
