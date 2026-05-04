# repobrain-community

Public install and community-facing surface for RepoBrain.

This repository is intended for:
- reusable GitHub workflows,
- community install templates,
- public-safe setup docs,
- bounded capability guidance.

It does not expose protected internal kernel details.

## External GitHub Foundation (Current)

Reusable workflow host:

- `.github/workflows/repobrain_external_foundation.yml`
- self-contained public host workflow (no runtime dependency on RepoBrain-Action)

Current bounded contract:

- supported: `/repobrain help`, `/repobrain ask ...`, `/repobrain review` (bounded Review-Lite PR triage)
- unsupported (explicit block): `/repobrain fix`, out-of-contract commands

Third-party caller workflow shape:

```yaml
jobs:
  repobrain_external:
    uses: alexworkingai/repobrain-community/.github/workflows/repobrain_external_foundation.yml@main
    with:
      dry_run: ${{ github.event_name == 'workflow_dispatch' && inputs.dry_run || 'false' }}
      comment_text: ${{ github.event_name == 'workflow_dispatch' && inputs.comment_text || github.event.comment.body }}
      issue_number: ${{ github.event_name == 'workflow_dispatch' && inputs.issue_number || github.event.issue.number }}
      workflow_path: .github/workflows/repobrain_external.yml
      caller_event_name: ${{ github.event_name }}
    secrets: inherit
```

## Community Trial Path

Use this short path for first external trial users:

1. Install or call the reusable workflow from `alexworkingai/repobrain-community/.github/workflows/repobrain_external_foundation.yml@main`.
2. Open a small PR in the target repository.
3. Run `/repobrain help`.
4. Run `/repobrain ask what is this PR about?`
5. Run `/repobrain review`.
6. Confirm `/repobrain fix` is blocked explicitly.

Bounded trial notes:

- Review-Lite is read-only PR triage.
- Ask and Review-Lite use visible repo/PR context only.
- No full review, fix generation, or security claims are made.
