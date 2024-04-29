# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.0] - 2024-04-20

### Added

- The `skip` input to skip on the callee's side of a `worfklow_call`. Otherwise, when the workflow is skipped from
  the caller's side (with an `if` expression), the check path when the workflow was run is not the same as when
  it was skipped ( `outer / inner` vs. `outer` when skipped) !

## [2.0.0] - 2024-01-19

### Removed

- The legacy file exporting the workflow. Now the workflow is only accessible at `.github/workflows/workflow.yml`.

## [1.1.0] - 2024-01-18

### Added

- A duplicate of the reusable workflow at the `.github/workflows/workflow.yml`. This is part of a change to have
  every reusable workflow exported under the same conventional path.

## [1.0.9] - 2024-01-16

### Changed

- Bunch of CI improvements.

### Fixed

- Correct the workflow reference in the `releasing` section of the README.

## [1.0.8] - 2023-12-29

### Fixed

- The email used with `git config`. It was improperly set to the user's name previously.

## [1.0.7] - 2023-12-19

### Fixed

- Turn off auto merging when merge conflicts are detected.

## [1.0.6] - 2023-12-19

### Fixed

- Check the merge command exit code before comparing git SHAs.

## [1.0.5] - 2023-12-18

### Fixed

- Invalid conditional expression using double quotes to refer to a literal string.

## [1.0.4] - 2023-12-18

### Fixed

- Dependency syntax between workflows.

## [1.0.3] - 2023-12-18

### Fixed

- Don't open a PR when the branch is already up-to-date.

## [1.0.2] - 2023-12-18

### Fixed

- The `fetch-depth` input to the `actions/checkout` action was incorrectly spelled.

## [1.0.1] - 2023-12-18

### Fixed

- Fixed the new branch name. There was a bug previously in the name of the output of a previous step.

## [1.0.0] - 2023-12-18

### Added

- First release!

[2.1.0]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.1.0...v2.0.0
[1.1.0]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.9...v1.1.0
[1.0.9]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.8...v1.0.9
[1.0.8]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.7...v1.0.8
[1.0.7]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.6...v1.0.7
[1.0.6]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.5...v1.0.6
[1.0.5]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.4...v1.0.5
[1.0.4]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.3...v1.0.4
[1.0.3]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.2...v1.0.3
[1.0.2]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/infrastructure-blocks/merge-template-workflow/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/infrastructure-blocks/merge-template-workflow/releases/tag/v1.0.0
