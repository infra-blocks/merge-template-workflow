# merge-template-workflow
[![Git Tag Semver From Label](https://github.com/infrastructure-blocks/merge-template-workflow/actions/workflows/git-tag-semver-from-label.yml/badge.svg)](https://github.com/infrastructure-blocks/merge-template-workflow/actions/workflows/git-tag-semver-from-label.yml)
[![Update From Template](https://github.com/infrastructure-blocks/merge-template-workflow/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/merge-template-workflow/actions/workflows/update-from-template.yml)

<<<<<<< HEAD
This repository offers a reusable workflow to merge template repositories. It is meant to be used in a `workflow_dispatch`
event.

It infers the template repository of the calling repository and merges its latest version from its default
branch into a new merge branch. When there are conflicts, the conflicting files are stored in a separate commit
for later review.

The merge branch is then opened as a pull request using the provided PAT so that it triggers other workflows.
The merge branch is automatically approved and auto-merge is enabled on it as well.

Updates without conflicts get automatically merged.
=======
This repository is a template for creating reusable GitHub Actions Workflows. Go through the below checklist
upon instantiating this template:
- Remove the [trigger update from template workflow](.github/workflows/trigger-update-from-template.yml)
- Edit the content of [the placeholder](.github/workflows/workflow.yml) for your reusable workflow.
- Update the status badges:
    - Remove the `Trigger Update From Template` status badge.
    - Add the `Update From Template` status badge.
    - Rename the rest of the links to point to the right repository.
- Edit this document and update the relevant sections
- Prepare the [changelog](CHANGELOG.md) for the first version of the module that will be released.
>>>>>>> template/master

## Inputs

|        Name         | Required | Description                                                                                                                                                                  |
|:-------------------:|:--------:|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| template-repository |  false   | The template repository to merge into the calling repository. The default is to infer by querying the current repository's template repository.                              |
|       labels        |  false   | A stringified JSON array of the labels to apply to the new PR. The values are label names. The default is "[]"                                                               | 
|        skip         |  false   | A boolean indicating whether to skip the workflow. This is to workaround the required checks discrepancy when the workflow is skipped from the caller. It defaults to false. |

## Secrets

|    Name    | Required | Description                                                                                                                                                                                                                                                                    |
|:----------:|:--------:|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| github-pat |   true   | The personal access token used to configure the git cli and make API calls to GitHub. The operations include fetching the template repository's code, listing the organization's repositories and opening a pull request. The approval is done through the Github Actions bot. |

## Outputs

N/A

## Permissions

|     Scope     | Level | Reason                                                                    |
|:-------------:|:-----:|---------------------------------------------------------------------------|
| pull-requests | write | To approve the newly created pull request through the GitHub Actions bot. |

## Concurrency controls

|       Field        |                  Value                   |
|:------------------:|:----------------------------------------:|
|       group        | ${{ github.workflow }}-${{ github.ref }} |
| cancel-in-progress |                   true                   |

## Timeouts

N/A

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
    uses: infrastructure-blocks/merge-template-workflow/.github/workflows/workflow.yml@v1
    with:
      labels: ${{ inputs.labels }}
    secrets:
      github-pat: ${{ secrets.PAT }}
```

### Releasing

The releasing is handled at git level with semantic versioning tags. Those are automatically generated and managed
by the [git-tag-semver-from-label-workflow](https://github.com/infrastructure-blocks/git-tag-semver-from-label-workflow).
