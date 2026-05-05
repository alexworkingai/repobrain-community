# repobrain-community

Public install kit for RepoBrain Community.

Use this repository when you want a first external GitHub-native RepoBrain setup that is:

- copyable,
- bounded,
- public-safe,
- easy to trial on a small PR.

## RepoBrain Community Preview

What works now:

- copyable install template
- `/repobrain doctor`
- `/repobrain ask ...`
- `/repobrain review` as bounded read-only Review Candidate
- `/repobrain fix` as bounded Fix-Lite Candidate manual patch suggestion
- optional repo guidance from `.github/repobrain.instructions.md` or `AGENTS.md`

Known limits:

- Fix-Lite Candidate is manual-only and may return `suggestion available`, `blocked`, or `not applicable`
- no patch application, file modification, commit creation, branch push, or PR creation
- Review Candidate is bounded and read-only
- output quality depends on visible PR/repo context
- guidance quality depends on short useful repo instructions
- no bug or security verdicts
- no full external review parity claim

## What This Supports

Supported:

- `/repobrain help`
- `/repobrain doctor`
- `/repobrain ask ...`
- `/repobrain review` as bounded read-only Review Candidate
- `/repobrain fix` as bounded Fix-Lite Candidate manual patch suggestion

Unsupported:

- out-of-contract commands

## Quick Install

1. Copy `templates/repobrain.yml` into your own repository as `.github/workflows/repobrain.yml`.
2. Optionally copy `templates/repobrain.instructions.md` into `.github/repobrain.instructions.md`.
3. Commit the workflow file.
4. Open a small PR in your repository.
5. Run `/repobrain doctor`.
6. Run `/repobrain help`.
7. Run `/repobrain ask what is this PR about?`
8. Run `/repobrain review`.
9. Run `/repobrain fix`.
10. Confirm no patch was applied and no files were modified.

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

## First External User Path

1. Copy `templates/repobrain.yml` into `.github/workflows/repobrain.yml`.
2. Optionally copy `templates/repobrain.instructions.md` into `.github/repobrain.instructions.md`.
3. Open a small PR.
4. Run `/repobrain doctor`.
5. Run `/repobrain ask what is this PR about?`
6. Run `/repobrain review`
7. Run `/repobrain fix`
8. Interpret the Fix-Lite Candidate outcome

Fix-Lite Candidate outcomes:

- `suggestion available` means RepoBrain found a narrow manual patch direction worth trying
- `blocked` means the visible scope is too broad or sensitive for a safe manual patch suggestion
- `not applicable` means no safe manual target was identifiable from bounded visible context

Blocked and not-applicable outcomes are healthy bounded behavior, not necessarily errors.

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
Supported: help · doctor · ask · review · fix-lite-candidate
Unsupported: out-of-contract commands
Setup notes:
- one RepoBrain responder is expected
- Surface supports bounded read-only Review Candidate
- Fix-Lite Candidate is manual-only and does not apply patches, modify files, or create commits
- answers use visible repo/PR context only
- if duplicate comments appear, check that only one workflow listens to `/repobrain` issue_comment
Next step: /repobrain ask what is this PR about?
```

`/repobrain review`

```text
## RepoBrain Review Candidate
PR Summary: Add TRIAL_PR_MARKER.md for validation PR marker.
Signal: basis=PR · scope=small · type=docs · context=strong
Changed files: TRIAL_PR_MARKER.md
Change areas: docs / validation
Guidance: prefer small PRs for external RepoBrain validation.
Attention: low based on visible change surface

Review focus:
- Small validation/docs change with limited visible scope.
- Repo guidance prefers small PRs and de-emphasizes generated/artifact files.
Review observations:
- This PR appears validation-only and low-scope based on visible changed files.
- Repo guidance prefers small PRs for external validation, which matches this change.
- Limited diff context was available, so observations stay surface-level.

Manual inspection points:
- Confirm the PR intent matches the visible changed files.
- Confirm this validation marker is intentionally part of the validation flow.

Evidence:
- changed files: 1
- change areas: docs / validation
- guidance: .github/repobrain.instructions.md
- diff context: limited snippets available
Bounded limits: read-only review; no fix generation; no security verdict.
Next safe step: /repobrain fix
```

`/repobrain fix`

```text
## RepoBrain Fix-Lite Candidate
Mode: manual-only patch suggestion
Status: suggestion available
Target: README.md
Suggested change type: documentation wording
Patch suggestion:
- In `README.md`, clarify the setup step to mention copying `templates/repobrain.yml`.
- Keep the edit limited to the visible changed section rather than expanding the PR scope.
Why bounded: single text-based documentation file, small visible change surface, no runtime code touched.
Guidance: prefer small PRs for external RepoBrain validation.
Signal: basis=PR · scope=small · type=docs · context=strong
No patch was applied. No files were modified.
Next safe step: apply manually, then run /repobrain review again.
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
- run `/repobrain fix`
- confirm no patch was applied and no files were modified
- verify one response per command
- verify no full review/fix/security claims are made

## Support And Feedback

If something looks wrong, open a GitHub issue and include:

- repository name
- command used
- expected result
- actual result
- workflow run link
- whether duplicate comments appeared
- whether `.github/repobrain.instructions.md` or `AGENTS.md` is present

If you want a ready-made report format, use `.github/ISSUE_TEMPLATE/repobrain-community-feedback.md`.

## Release Validation Matrix

| Command | Expected result |
|---|---|
| `/repobrain doctor` | One response, guidance status shown if present, supported commands include fix-lite-candidate |
| `/repobrain help` | One response, command truth matches current bounded surface |
| `/repobrain ask what is this PR about?` | One response, compact PR-aware answer |
| `/repobrain review` | One response, Review Candidate card with focus, observations, manual inspection points, and evidence |
| `/repobrain fix` | One response, Fix-Lite Candidate card with no-action guarantee |

Also verify:

- no duplicate comments
- README/template examples match live behavior
- no autofix, patch-application, bug, or security-review claims appear

## Bounded Notes / Non-Claims

- `/repobrain doctor` verifies the external setup surface only.
- `/repobrain doctor` does not repair workflows or installation problems.
- Repo guidance is optional and limited to `.github/repobrain.instructions.md` and `AGENTS.md`.
- Review Candidate is bounded read-only external review.
- Review Candidate uses visible PR context, limited diff context, and repo guidance.
- Fix-Lite Candidate is bounded manual-only patch suggestion guidance.
- Ask and review use visible repo/PR context only.
- Fix-Lite Candidate does not apply patches, modify files, create commits, push branches, or open PRs.
- No full external review parity is claimed.
- No bug finding claims are made.
- No vulnerability/security claims are made.
- No patch generation or autofix behavior is performed.
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
