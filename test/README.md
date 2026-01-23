# GitHub Action Test

<!-- prettier-ignore-start -->
<!-- action-docs-description -->
## Description

GitHub Action that runs unit tests present within a JVM based (e.g. Java) GitHub repository and report test coverage metrics.
<!-- action-docs-description -->
<!-- prettier-ignore-end -->

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

### Disabling Gradle cache

```yaml
jobs:
  test:
    steps:
      - name: Test
        uses: open-turo/actions-jvm/test@v1
        with:
          gradle-cache-enabled: false
```

<!-- prettier-ignore-start -->
<!-- action-docs-inputs -->
## Inputs

| parameter | description | required | default |
| --- | --- | --- | --- |
| checkout-repo | Perform checkout as first step of action | `false` | true |
| github-token | GitHub token that can checkout the repository. e.g. 'secrets.GITHUB_TOKEN' | `true` |  |
| artifactory-username | Username to use for Artifactory access | `true` |  |
| artifactory-auth-token | Authentication token to use with username for Artifactory access | `true` |  |
| gradle-task | An optional string for the gradle test task to run. e.g. "integrationTest" | `false` | test |
| gradlew-args | An optional string of command line arguments to pass to gradlew. e.g. "--debug" | `false` |  |
| gradle-cache-enabled | Whether to enable Gradle caching via gradle/actions/setup-gradle | `false` | true |
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

## Test

It will run to detect and execute all unit tests in the top level of the
repository and all subdirectories.

```shell
gradelw test -PartifactoryUsername=?? -PartifactoryAuthToken=??
```

## Notes

- By default, this action will perform actions/checkout as its first step.
- This action uses [gradle/actions/setup-gradle](https://github.com/gradle/actions/blob/main/docs/setup-gradle.md) for Gradle dependency caching to improve build performance.
- Repositories using this action are expected to include a Gradle wrapper (`gradlew` and `gradle/wrapper/`) in their codebase.
