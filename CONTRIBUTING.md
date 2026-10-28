# Contributing to `seekdb`

Thanks for taking the time to contribute. This document describes the kinds of contributions we welcome and the expectations for each of them.

# Types of Contributions

## Report Bugs

Open an issue with:

- the version or commit you are running,
- the exact SQL or command that triggers the problem,
- what you expected and what happened instead,
- logs, stack traces, or `EXPLAIN` output where relevant.

A minimal reproduction is worth more than a long description. If you can reduce the case to a single table and one statement, do that first.

## Fix Bugs

Look for issues labeled `bug` or `good first issue`. Comment on the issue before starting so two people do not work on the same fix. A bug fix should come with a regression test that fails before the change and passes after it.

## Implement Features

Open an issue describing the use case before writing a large feature. Explain who needs it, what the alternative is today, and how it fits the existing architecture. Small, self-contained features can go straight to a pull request.

## Write Documentation

Documentation fixes, clarifications, and new examples are always welcome, and they do not need an issue first. Keep the tone concrete: show the command, show the output.

## Submit Feedback

If you use seekdb and something is awkward, say so in an issue or a discussion. Usability feedback about SQL behavior, error messages, and defaults is especially useful.

# Get Started!

1. Read [AGENTS.md](AGENTS.md) for repository layout, build commands, and coding conventions.
2. Read [REVIEW.md](REVIEW.md) to understand how your change will be judged.
3. Build the project locally and run the relevant test directory before opening a pull request.
4. Fork, branch from the default branch, commit, and open the pull request.

# Pull Request Guidelines

- **One concern per pull request.** A bug fix plus a refactor is two pull requests.
- **Describe the behavior, not just the diff.** Say what was wrong, why the change fixes it, and how you verified it.
- **Include tests.** New behavior needs coverage; fixed behavior needs a regression case.
- **Keep the diff reviewable.** Prefer a stack of small commits over one large commit with an unrelated cleanup at the end.
- **Note the risk.** Call out anything that changes on-disk format, network protocol, or default configuration.
- **Reference the issue.** Use `Fixes #123` so the issue closes when the pull request merges.
