# CLAUDE.md

Project memory. Read it fully before touching a file; keep it current when something here
turns out to be wrong.

## Stack

- <!-- language / runtime / version, e.g. Python 3.12 -->
- <!-- framework, package manager, test runner -->
- <!-- services this talks to, and whether they are mocked in tests -->

## Layout

```
src/        application code
tests/      pytest, mirrors src/ one-to-one
scripts/    one-off entry points, never imported by src
```

## Commands

| Task | Command |
| --- | --- |
| install deps | `<!-- ... -->` |
| run tests | `<!-- pytest -q -->` |
| lint + types | `<!-- ruff check . && mypy src -->` |
| run locally | `<!-- ... -->` |

## Conventions

- Match the surrounding code: naming, error handling, logging. No new patterns for one call site.
- Types on public functions. No `Any` without a comment saying why.
- Errors get context (`raise ... from exc`), never a bare `except:`.
- New behaviour gets a test in the same commit. Bug fixes get a test that fails first.
- Small diffs. If a change needs a paragraph to justify, split it.

## Rules

- Do not reformat files you only partly touched.
- Do not edit `.env*`, lockfiles or migrations by hand unless asked.
- Never `git push --force`, `git reset --hard`, or `rm -rf` without saying so first.
- Never delete or skip a failing test to make the suite green — report it.
- If a command fails twice, stop and show the error instead of retrying variants.
- Ask before adding a dependency.

## Definition of done

1. `<!-- test command -->` passes.
2. Lint and types are clean.
3. Diff contains only the requested change plus its tests.
4. You stated what you did not verify.

## Notes

<!-- domain quirks, timezone/unit conventions, gotchas in the build, known flaky tests -->
