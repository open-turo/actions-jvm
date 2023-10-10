# GitHub Action Test

## Description

GitHub Action that runs unit tests present within a JVM based (e.g. Java) GitHub repository and report test coverage metrics.

## Usage

### Basic

```yaml
jobs:
  test:
    steps:
      - name: Test
        uses: open-turo/actions-jvm/test@v1
```

### Enabling debug output in test

```yaml
jobs:
  test:
    steps:
      - name: Test
        uses: open-turo/actions-jvm/test@v1
        with:
          gradlew-args: --debug
```

### Running specific test task

```yaml
jobs:
  test:
    steps:
      - name: Test
        uses: open-turo/actions-jvm/test@v1
        with:
          gradle-task: integrationTest
```

## Inputs

| parameter              | description                                                                     | required | default |
| ---------------------- | ------------------------------------------------------------------------------- | -------- | ------- |
| checkout-repo          | Perform checkout as first step of action                                        | `false`  | true    |
| github-token           | GitHub token that can checkout the repository. e.g. 'secrets.GITHUB_TOKEN'      | `true`   |         |
| artifactory-username   | Username to use for Artifactory access                                          | `true`   |         |
| artifactory-auth-token | Authentication token to use with username for Artifactory access                | `true`   |         |
| gradle-task            | An optional string for the gradle test task to run. e.g. "integrationTest"      | `false`  | `test`  |
| gradlew-args           | An optional string of command line arguments to pass to gradlew. e.g. "--debug" | `false`  |         |

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
