# GitHub Action Test

## Description

GitHub Action that runs unit tests present within a JVM based (e.g. Java) GitHub repository and report test coverage metrics.

## Usage

```yaml
jobs:
  test:
    steps:
      - name: Test
        uses: open-turo/actions-jvm/test@v1
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

## Test

It will run to detect and execute all unit tests in the top level of the
repository and all subdirectories.

```shell
gradelw test -PartifactoryUsername=?? -PartifactoryAuthToken=??
```

## Notes

- By default, this action will perform actions/checkout as its first step.
