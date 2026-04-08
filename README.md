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

Current bounded contract:

- supported: `/repobrain help`, `/repobrain ask ...`
- unsupported (explicit block): `/repobrain review`, `/repobrain fix`, out-of-contract commands

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
