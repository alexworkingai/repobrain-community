# repobrain-community

Public install kit for RepoBrain Community.

Use this repository when you want a first external GitHub-native RepoBrain setup that is:

- copyable,
- bounded,
- public-safe,
- easy to trial on a small PR.

## What This Supports

Supported:

- `/repobrain help`
- `/repobrain doctor`
- `/repobrain ask ...`
- `/repobrain review` as bounded read-only Review v1

Unsupported:

- `/repobrain fix`
- out-of-contract commands

## Quick Install

1. Copy `templates/repobrain.yml` into your own repository as `.github/workflows/repobrain.yml`.
2. Commit the workflow file.
3. Open a small PR in your repository.
4. Run `/repobrain doctor`.
5. Run `/repobrain help`.
6. Run `/repobrain ask what is this PR about?`
7. Run `/repobrain review`.
8. Confirm `/repobrain fix` is blocked explicitly.

The reusable workflow host is:

- `alexworkingai/repobrain-community/.github/workflows/repobrain_external_foundation.yml@main`

## Copyable Workflow Template

- template file: `templates/repobrain.yml`

This template:

- supports `issue_comment` command entry,
- supports `workflow_dispatch` for manual testing,
- calls the canonical public host in this repository,
- does not rely on private/internal runtime wiring.

Optional repo guidance:

- RepoBrain can also read `.github/repobrain.instructions.md`
- RepoBrain can use `AGENTS.md` when present
- sample guidance file: `templates/repobrain.instructions.md`

## Expected Output Examples

`/repobrain ask what is this PR about?`

```text
## RepoBrain Ask
Question: what is this PR about?
Answer: Add TRIAL_PR_MARKER.md for validation PR marker.
Signal: basis=PR · scope=small · type=docs · context=strong
Changed files: TRIAL_PR_MARKER.md
```

`/repobrain ask what should I pay attention to here?`

```text
## RepoBrain Ask
Question: what should I pay attention to here?
Answer: This PR touches deployment config. Repo guidance marks deployment/config changes as caution areas.
Signal: basis=PR · scope=small · type=config · context=strong
Guidance: check deployment-related assumptions before merge
Changed files: TRIAL_PR_MARKER.md
```

`/repobrain doctor`

```text
## RepoBrain Doctor
Status: connected
Surface: external GitHub foundation
Host: repobrain-community@main
Workflow: .github/workflows/repobrain.yml
Event: issue_comment
Guidance: found .github/repobrain.instructions.md
Supported: help · doctor · ask · review
Unsupported: fix
Setup notes:
- one RepoBrain responder is expected
- Surface supports bounded read-only Review v1
- answers use visible repo/PR context only
- if duplicate comments appear, check that only one workflow listens to `/repobrain` issue_comment
Next step: /repobrain ask what is this PR about?
```

`/repobrain review`

```text
## RepoBrain Review
PR Summary: Add TRIAL_PR_MARKER.md for validation PR marker.
Signal: basis=PR · scope=small · type=docs · context=strong
Changed files: TRIAL_PR_MARKER.md
Change areas: docs / validation
Guidance: repo instructions mark deployment/config changes as caution areas
Review observations:
- This PR appears validation-only and low-scope based on visible changed files.
- Repo guidance prefers small PRs for external validation, which matches this change.
Bounded limits: read-only review; no fix generation; no security verdict.
Next safe step: /repobrain ask what changed here?
```

`/repobrain fix`

```text
RepoBrain external GitHub mode foundation currently supports `/repobrain help`, `/repobrain doctor`, `/repobrain ask`, and bounded `/repobrain review`.
Received: `/repobrain fix`.
This bounded behavior is intentional for the current external GitHub foundation stage.
```

## Community Trial Checklist

- copy `templates/repobrain.yml` into `.github/workflows/repobrain.yml`
- open a small PR
- run `/repobrain doctor`
- run `/repobrain help`
- optionally add `.github/repobrain.instructions.md`
- run `/repobrain ask what is this PR about?`
- run `/repobrain ask what should I pay attention to here?`
- run `/repobrain review`
- confirm `/repobrain fix` is blocked
- verify one response per command
- verify no full review/fix/security claims are made

## Bounded Notes / Non-Claims

- `/repobrain doctor` verifies the external setup surface only.
- `/repobrain doctor` does not repair workflows or installation problems.
- Repo guidance is optional and limited to `.github/repobrain.instructions.md` and `AGENTS.md`.
- Review v1 is bounded read-only external review.
- Ask and review use visible repo/PR context only.
- No full external review parity is claimed.
- No bug finding claims are made.
- No vulnerability/security claims are made.
- No fix suggestions or patch generation are performed.
- No autonomous agent behavior is claimed.


## Optional Repo Guidance Example

Copy one of these files into your repository when you want short repo-specific hints:

- `.github/repobrain.instructions.md`
- `AGENTS.md`

Example:

```md
Review priorities:
- Treat auth and deployment changes as high attention.
- Prefer small PRs.
- Generated files should not drive review focus.

Build/test hints:
- Run npm test for app changes.
- Run npm run lint for TypeScript changes.
```
