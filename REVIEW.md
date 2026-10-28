# Code review guidelines

This document describes what a reviewer looks for in a seekdb change. It is also a checklist for authors before they open a pull request.

## Establish the behavior

Before reading the diff, state what the current behavior is and what the new behavior should be. A change that cannot be described in one sentence of behavior is usually two changes.

For a bug fix, identify the failing input and the expected output. For a feature, identify the caller and the contract.

## Separate defects from design choices

Ask two different questions, in this order:

1. **Is this wrong?** Uninitialized reads, missed error codes, broken invariants, off-by-one bounds, missing `nullptr` checks.
2. **Would I have built it this way?** This is a preference, and it should be labeled as one.

Do not let a design preference be written up as a defect. If the author's choice is defensible, say so and move on, even when you would have chosen differently.

## Check corresponding implementations

Many paths in seekdb exist twice: a local and a distributed form, a row store and a column store form, a write path and a replay path. When a change touches one, check whether the counterpart needs the same fix. A fix applied to only half of a pair is a future bug report.

Pay particular attention to:

- error handling on every branch that can fail, not only the happy path,
- lifetime of objects handed to background tasks or threads,
- behavior under restart, replay, and rollback,
- memory accounting, so a new allocation is counted where its peers are counted.

## Write useful comments

A review comment should say what to change and why, and it should be actionable by someone reading only that comment.

- Quote the line, describe the concrete scenario, and propose the fix.
- Distinguish blocking problems from suggestions: prefix non-blocking notes with `nit:` or `optional:`.
- If you are unsure, ask a question instead of asserting.
- Approve when the change is correct and safe. Perfect is not the bar, and blocking on style alone wastes the author's time.
