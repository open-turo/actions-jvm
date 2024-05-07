# GitHub Action Lint

<!-- prettier-ignore-start -->
<!-- action-docs-description -->
## Description

GitHub Action to lint a JVM based repository
<!-- action-docs-description -->
<!-- prettier-ignore-end -->

## Usage

```yaml
jobs:
  build:
    steps:
      - name: Action lint
        uses: open-turo/actions-jvm/lint@v1
```

## Lint Checks

This action runs the following lint checks:

- [wagoid/commitlint-github-action](https://github.com/wagoid/commitlint-github-action)
- [pre-commit/action](https://github.com/pre-commit/action)

## Notes

- By default, this action will perform actions/checkout as its first step.
- This expects that `.commitlintrc.yaml` will be present to enforce [`conventional-commit`](https://github.com/wagoid/commitlint-github-action).

<!-- prettier-ignore-start -->
<!-- action-docs-inputs -->
## Inputs

| parameter | description | required | default |
| --- | --- | --- | --- |
| checkout-repo | Perform checkout as first step of action | `false` | true |
| github-token | GitHub token that can checkout the repository. e.g. 'secrets.GITHUB_TOKEN' | `true` |  |
| artifactory-username | Username to use for Artifactory access | `true` |  |
| artifactory-auth-token | Authentication token to use with username for Artifactory access | `true` |  |
<!-- action-docs-inputs -->

<!-- action-docs-outputs -->

<!-- action-docs-outputs -->

<!-- action-docs-runs -->
## Runs

This action is a `composite` action.
<!-- action-docs-runs -->

<!-- action-docs-usage  -->
<!-- action-docs-usage -->
<!-- prettier-ignore-end -->
