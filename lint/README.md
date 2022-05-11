# GitHub Action Lint

## Description

GitHub Action to lint a JVM based repository

## Usage

```yaml
jobs:
  build:
    steps:
      - name: Action lint
        uses: open-turo/actions-jvm/lint@v1
```

## Inputs

| parameter              | description                                                                | required | default |
| ---------------------- | -------------------------------------------------------------------------- | -------- | ------- |
| checkout-repo          | Perform checkout as first step of action                                   | `false`  | true    |
| github-token           | GitHub token that can checkout the repository. e.g. 'secrets.GITHUB_TOKEN' | `true`   |         |
| artifactory-username   | Username to use for Artifactory access                                     | `true`   |         |
| artifactory-auth-token | Authentication token to use with username for Artifactory access           | `true`   |         |

## Runs

This action is an `composite` action.

## Lint Checks

This action runs the following lint checks:

- [wagoid/commitlint-github-action](https://github.com/wagoid/commitlint-github-action)
- [pre-commit/action](https://github.com/pre-commit/action)

## Notes

- By default, this action will perform actions/checkout as its first step.
- This expects that `.commitlintrc.yaml` will be present to enforce [`conventional-commit`](https://github.com/wagoid/commitlint-github-action).
