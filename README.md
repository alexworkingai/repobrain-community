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
- `/repobrain ask ...`
- `/repobrain review` as bounded Review-Lite PR triage

Unsupported:

- `/repobrain fix`
- out-of-contract commands

## Quick Install

1. Copy `templates/repobrain.yml` into your own repository as `.github/workflows/repobrain.yml`.
2. Commit the workflow file.
3. Open a small PR in your repository.
4. Run `/repobrain help`.
5. Run `/repobrain ask what is this PR about?`
6. Run `/repobrain review`.
7. Confirm `/repobrain fix` is blocked explicitly.

The reusable workflow host is:

- `alexworkingai/repobrain-community/.github/workflows/repobrain_external_foundation.yml@main`

## Copyable Workflow Template

- template file: `templates/repobrain.yml`

This template:

- supports `issue_comment` command entry,
- supports `workflow_dispatch` for manual testing,
- calls the canonical public host in this repository,
- does not rely on private/internal runtime wiring.

## Expected Output Examples

`/repobrain ask what is this PR about?`

```text
## RepoBrain Ask
Question: what is this PR about?
Answer: Add TRIAL_PR_MARKER.md for validation PR marker.
Signal: basis=PR · scope=small · type=docs · context=strong
Changed files: TRIAL_PR_MARKER.md
```

`/repobrain review`

```text
## RepoBrain Review-Lite
PR Summary: Add TRIAL_PR_MARKER.md for validation PR marker.
Signal: basis=PR · scope=small · type=docs · context=strong
Changed files: TRIAL_PR_MARKER.md
Watch points:
- read-only triage based on visible PR context
- no deep code review, fix generation, or security claims performed
Next safe step: /repobrain ask what changed here?
```

`/repobrain fix`

```text
RepoBrain external GitHub mode foundation currently supports `/repobrain help`, `/repobrain ask`, and bounded `/repobrain review`.
Received: `/repobrain fix`.
This bounded behavior is intentional for the current external GitHub foundation stage.
```

## Community Trial Checklist

- copy `templates/repobrain.yml` into `.github/workflows/repobrain.yml`
- open a small PR
- run `/repobrain help`
- run `/repobrain ask what is this PR about?`
- run `/repobrain review`
- confirm `/repobrain fix` is blocked
- verify one response per command
- verify no full review/fix/security claims are made

## Bounded Notes / Non-Claims

- Review-Lite is read-only PR triage.
- Ask and Review-Lite use visible repo/PR context only.
- No full external review parity is claimed.
- No bug finding claims are made.
- No vulnerability/security claims are made.
- No fix suggestions or patch generation are performed.
- No autonomous agent behavior is claimed.
