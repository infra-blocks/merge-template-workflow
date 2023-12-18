# merge-template-workflow

This repository offers a reusable workflow to merge template repositories. It is meant to be used in a `workflow_dispatch`
event.

It infers the template repository of the calling repository and merges its latest version from its default
branch into a new merge branch. When there are conflicts, the conflicting files are stored in a separate commit
for later review.

The merge branch is then opened as a pull request using the provided PAT so that it triggers other workflows.
The merge branch is automatically approved and auto-merge is enabled on it as well.

Updates without conflicts get automatically merged.

## Usage

```yaml
name: Update From Template

on:
  workflow_dispatch:
    inputs:
      labels:
        description:
          A stringified JSON array of labels to apply to the PR.
        required: false
        default: '[]'
        type: string

permissions:
  # Required to approve pull request with GITHUB_TOKEN
  pull-requests: write

jobs:
  merge-template:
    uses: infrastructure-blocks/merge-template-workflow/.github/workflows/merge-template.yml@v1
    with:
      labels: ${{ inputs.labels }}
    secrets:
      github-pat: ${{ secrets.PAT }}
```

### Releasing

The releasing is handled at git level with semantic versioning tags. Those are automatically generated and managed
by the [git-tag-semver-from-label-action](https://github.com/infrastructure-blocks/git-tag-semver-from-label-action).
