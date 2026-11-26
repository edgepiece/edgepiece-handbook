# Standard repository configuration

Every Edgepiece repo is configured the same way. This note lists each setting and the reason for it. Settings are applied through the GitHub API and compared across repos, not set by hand in the UI.

## Merge settings
| Setting | Value | Why |
|---|---|---|
| Squash merge | On | One PR becomes one commit on `main`. History reads as a list of changes. |
| Merge commit, rebase merge | Off | Only one way to merge, so history is uniform. |
| Squash commit title | PR title | The PR title is a conventional commit and release automation reads it. |
| Squash commit message | Blank | Drops the PR body and any co-author trailers from `main`. |
| Delete head branches on merge | On | No stale branches. |

Consequence of the blank message: a `BREAKING CHANGE:` footer in a PR body is dropped. A breaking change is marked with `!` in the PR title (`feat!: ...`).

## Ruleset `protect-main`
Applies to the default branch. No bypass actors, so admins follow the same rules.

| Rule | Why |
|---|---|
| Pull request required | No direct pushes to `main`. |
| Allowed merge method: squash | Matches the merge settings. |
| Zero required approvals | One-person org. Review happens at merge. Raise this when there is a second reviewer. |
| Dismiss stale reviews on push | An approval does not carry over to code that changed after it. |
| Linear history | No merge commits on `main`. |
| Block force pushes and deletion | `main` cannot be rewritten or removed. |
| Required status checks | The checks that prove a change is safe (see below). |
| Branches must be up to date | Checks run against what `main` will actually contain after the merge. |

## Required checks
Each repo requires the checks that apply to it. A check is added to the ruleset when it lands.

| Check | Repos |
|---|---|
| `pr-title` | All |
| `lint` | Repos with a Dockerfile or workflows |
| `build-and-smoke-test` | Repos that build an image |
| `release-dry-run` | Repos that release |

Required checks are matched by job name. A job that is skipped counts as passing, so a skipped job is never proof a check ran.

## Known gaps
- Branch protection on private repos needs a paid plan. Edgepiece repos are public.
- `edgepiece-handbook` has no ruleset yet.

## New repo checklist
1. Create the repo (public, MIT license).
2. Set the merge settings above.
3. Create the `protect-main` ruleset with no required checks.
4. Prove it: a direct push to `main` is rejected.
5. Add each required check to the ruleset as it lands. Prove each one turns red on a throwaway PR.
6. Add the repo to the org Project and the workspace file.
