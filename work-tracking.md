# Work tracking

How work is requested, tracked and shipped. Applies to every Edgepiece repo.

## Principles
- Every change starts from an issue.
- Work that surfaces mid-task becomes a new issue. It does not grow the current PR.
- One issue, one branch, one PR. A PR is one atomic change that is safe to release on its own.
- Small and frequent. Target review turnaround is 1 to 2 days. A larger change is split into sub-issues.

## Where things live
- Issues live in the repo that owns the work.
- One org-level GitHub Project, "Edgepiece", shows issues from all repos.
- Requests between teams (for example, to Platform) are issues in the owning team's repo.
- Product slices (see [business.md](business.md)) are parent issues. Their pieces are sub-issues.

## Issues
- Type: Bug, Feature or Task (GitHub issue types).
- Title states the outcome in plain language.
- Body gives the context and the acceptance criteria: how we know it is done.
- An unrelated problem found during other work gets its own issue, linked to the current one. It is not fixed in place.

## Project statuses
| Status | Meaning |
|---|---|
| Todo | Captured. Not started. |
| In Progress | A branch or an open PR exists. |
| Done | Merged and the issue is closed. |

## Branches and pull requests
- Branch from `main`: `<issue-number>-short-description`. Short-lived.
- PR title is a conventional commit (`type(scope): description`). It becomes the squash commit message, and release automation reads it. A `pr-title` check enforces the format.
- PR body links the issue with `Closes #<number>`.
- Required checks must pass before merge. Direct pushes to `main` are blocked where branch protection is enabled.

## Done
Merged, checks green, issue closed, and released if the change affects a released artifact.

## Releases
Merging to `main` releases automatically (semantic-release). Release notes are generated from commit titles.
