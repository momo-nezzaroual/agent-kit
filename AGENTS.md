# AGENTS.md

Tool-agnostic project rules. If your agent reads `CLAUDE.md`, this file only needs to point
at it; if it does not, the short version lives here.

## Read first

`CLAUDE.md` — stack, layout, commands, conventions.

## Non-negotiables

- Read a file before editing it. Read the tests too.
- New behaviour ships with a test; bug fixes ship with the failing test that proves them.
- Keep diffs scoped to the request. No drive-by reformatting.
- Run the test command from `CLAUDE.md` before claiming anything works.
- Do not touch `.env*`, lockfiles or migrations by hand unless asked.
- No `git push --force`, `git reset --hard` or `rm -rf` without warning.
- Two failed retries on the same command → stop, show the error, ask.

## Report format

Finish with: what changed, how it was verified, what is still unverified or out of scope.
