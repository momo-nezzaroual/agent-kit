# agent-kit

A small, opinionated starting point for wiring an AI coding agent into a repo: persistent
project memory, guard rails, and a couple of repeatable commands.

Works with Claude Code, Codex, Cursor and anything else that reads `AGENTS.md`.

## Files

| File | Purpose |
| --- | --- |
| `CLAUDE.md` | project memory the agent reads every session — stack, layout, commands, rules |
| `AGENTS.md` | tool-agnostic pointer so non-Claude agents get the same rules |
| `settings.example.json` | permission allow/deny lists + env, copied to `.claude/settings.json` |
| `command-review.md` | `/review` — correctness and risk pass over the working diff |
| `command-ship.md` | `/ship` — tests, changelog, commit, PR body, then stop before pushing |

## Install

```bash
mkdir -p .claude/commands
cp CLAUDE.md AGENTS.md .
cp settings.example.json .claude/settings.json
cp command-review.md .claude/commands/review.md
cp command-ship.md .claude/commands/ship.md
```

Then edit `CLAUDE.md`. A memory file the agent has to guess from is worse than none — write
the commands, the layout, and the three rules a new contributor always gets wrong.

## Why the guard rails

The agent is fast and confident. The failure modes are predictable too: runs `git push
--force`, reads `.env` into the transcript, rewrites a file it never opened, "fixes" a test
by deleting it. `settings.example.json` blocks the first two by default and the rest belong
in `CLAUDE.md` as hard rules, not suggestions.

Recommended baseline for the deny list (extend it per repo):

```json
"deny": [
  "Read(./.env)", "Read(./.env.*)", "Read(./secrets/**)",
  "Bash(git push --force:*)", "Bash(git reset --hard:*)",
  "Bash(rm -rf:*)", "Bash(sudo:*)"
]
```

## Rules of thumb

- Keep `CLAUDE.md` under ~100 lines. Long memory files get skimmed or ignored.
- Prefer one `/command` over a paragraph of prompt for anything you do more than twice.
- Give the agent a way to prove its work (`npm test`, `pytest -q`) and require it in the
  command files. "Looks right" is not a verification step.
- Review diffs, not summaries. Ask for the diff.

## License

MIT
## Notes

Longer memory files get skimmed.
