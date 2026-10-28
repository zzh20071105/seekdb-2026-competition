# Repository Guidelines

Guidance for contributors and coding agents working in this repository.

## Project Structure & Module Organization

- `src/` — the database kernel, organized by subsystem (`storage`, `sql`, `share`, `observer`, `rootserver`, `logservice`, `common`).
- `include/` — headers that the build exposes outside a single module.
- `deps/` — third-party dependencies, fetched by the build.
- `unittest/` — unit tests, one directory per module.
- `tools/obtest` — regression suite: `.test` cases in `t/`, expected output in `r/`.
- `docs/` — design notes and user-facing documentation.

Keep new code inside the existing subsystem that owns the behavior. Do not create a new top-level directory without an issue explaining why.

## Build, Test, and Development Commands

```bash
./build.sh --help      # list build flags
./build.sh             # build (first run fetches deps, takes a long time)
```

- Incremental builds reuse the existing build directory; do not wipe it unless the build is genuinely corrupted.
- Unit tests live under `unittest/`; regression cases under `tools/obtest`. Run the narrowest suite that covers your change before pushing.
- A change to the SQL layer should be exercised with a real statement, not only with a unit test.

## Coding Style & Naming Conventions

- C++20, 2-space indent, braces on their own line for functions.
- New classes do not need the legacy `Ob` prefix. Keep the `I` prefix for interfaces (`ICacheMemoryGetter`, not `ObICacheMemoryGetter`). Do not rename existing types only to drop `Ob`.
- Use `#pragma once` in new headers instead of `#ifndef` guards.
- Member variables keep the `_` suffix used by the surrounding file.
- Prefer `nullptr`, `override`, and scoped enums over their C-era equivalents.
- Error handling is by return code (`int`) throughout the kernel; check every one.

## Design and Implementation

- Match the shape of the nearest existing implementation rather than inventing a new pattern inside one function.
- Many paths exist twice (local/remote, row/columnar, write/replay). When you change one, check the counterpart.
- Anything handed to a background task needs an explicit lifetime story.
- New allocations should be accounted where their peers are accounted.

## Testing Guidelines

- Add a regression case for every bug fix; name it after the failure, not the fix.
- Unit tests go next to the module they test, under `unittest/`.
- Integration cases go in `tools/obtest/t/<area>/`, with expected output in `tools/obtest/r/<area>/`.
- Do not add benchmark-only files under `tools/` unless the task needs a reusable developer tool.

## Commit & Pull Request Guidelines

- One logical change per commit; one concern per pull request.
- Commit subject: imperative, under 72 characters, e.g. `fix: reject empty embedding arrays`.
- Body: what was wrong, why this fixes it, how it was verified.
- Pull requests state the behavior change first, the diff second, and any compatibility risk last.
- Reference the issue (`Fixes #123`) so it closes on merge.

## Security & Configuration Tips

- Never commit credentials, tokens, or internal endpoints. Use `.env`-style local files that are git-ignored.
- Default configuration must be safe: a fresh checkout should not bind to a public interface or disable authentication.
- When a change affects on-disk format, call it out explicitly in the pull request — it is the one thing that cannot be rolled back quietly.
