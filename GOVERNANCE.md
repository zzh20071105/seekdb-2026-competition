# seekdb Governance

This document describes how decisions are made in this repository, who is responsible for what, and how someone becomes a maintainer.

## Governance principles

- **Open by default.** Design discussions, review comments, and roadmap decisions happen in public issues and pull requests.
- **Merit over title.** Influence comes from sustained, high-quality contribution rather than from an appointment.
- **Reversible decisions move fast; irreversible ones move slowly.** A change in default configuration is cheap to undo. A change in on-disk format is not.
- **One voice, after the debate.** Once a decision is recorded, everyone implements it consistently, including the people who argued the other way.

## Governance structure and roles

### PMC responsibilities

The Project Management Committee owns the long-term direction of the project:

- approve or reject proposals that change architecture, on-disk format, or public SQL behavior,
- resolve disagreements that cannot be settled in a pull request thread,
- appoint maintainers and reviewers,
- keep this document and the role roster current.

### Maintainer responsibilities

Maintainers keep the project healthy day to day:

- review and merge pull requests in their area,
- triage issues and keep labels meaningful,
- watch build health, test flakiness, and release readiness,
- mentor new contributors and nominate reviewers.

## Decision making

### Routine changes

Bug fixes, documentation, tests, and localized improvements are decided by lazy consensus: a maintainer reviews, the CI is green, and no one objects within the review window. Silence on a pull request means consent.

### Substantial technical changes

A change counts as substantial when it touches on-disk format, network protocol, default configuration, a public SQL surface, or introduces a new subsystem.

For these, propose the change in an issue first. The proposal should state the problem, the alternatives considered, the cost of doing nothing, and the migration or compatibility story. The PMC records the outcome in the issue, and the reasoning is kept there rather than in a private chat.

## Contributor roles and appointments

### Becoming a Reviewer

Sustained contribution in one area, several merged pull requests of good quality, and demonstrated judgement in review comments. A maintainer nominates and the PMC confirms.

### Becoming a Maintainer

A reviewer who has consistently reviewed their area for some months, understands the architecture beyond a single module, and can be trusted to merge without supervision.

### Becoming a PMC member

A maintainer who takes responsibility for direction rather than execution: writing proposals, mediating disagreements, and representing the project outside the repository.

## Community participation and communication

- Technical discussion happens in issues, not in private messages.
- Questions are welcome; "read the source" is not an answer.
- Disagreement is expected and useful. Attack the design, never the person.
- Anything a newcomer needs to know should end up in the repository, not in a chat history.

## Member roster and document maintenance

### PMC members

Listed in the commit history and in the repository's `AUTHORS` information where it exists.

### Maintainers

Listed in the same place, by area of responsibility.

### Maintaining the roster and this document

Role changes take effect when the pull request that updates this document merges. If the roster and reality disagree, reality wins and the document is corrected.
