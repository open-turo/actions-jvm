# GitHub Action: Prerelease Version

<!-- prettier-ignore-start -->
<!-- action-docs-description -->
## Description

GitHub Action to compute a prerelease version based on the latest release version and the number of commits since the latest release.
<!-- action-docs-description -->
<!-- prettier-ignore-end -->

## Configuration

### Step1: Set any [Semantic Release Configuration](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#configuration) in your repository.

### Step2: [Add Secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) in your repository for the [Semantic Release Authentication](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/ci-configuration.md#authentication) Environment Variables.

### Step3: Add a [Workflow File](https://help.github.com/en/articles/workflow-syntax-for-github-actions) to your repository to create custom automated processes.

## Usage

```yaml
steps:
  - name: Action semantic release
    uses: open-turo/actions-jvm/prerelease@v1
    with:
      github-token: ${{ secrets.GITHUB_TOKEN }}
```

**IMPORTANT**: `GITHUB_TOKEN` does not have the required permissions to operate on protected branches.
If you are using this action for protected branches, replace `GITHUB_TOKEN`
with [Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line).
If using the `@semantic-release/git` plugin for protected branches, avoid persisting credentials as part
of `actions/checkout@v4` by setting the parameter `persist-credentials: false`. This credential does not have the
required permission to operate on protected branches.

<!-- prettier-ignore-start -->
<!-- action-docs-inputs -->
## Inputs

| parameter | description | required | default |
| --- | --- | --- | --- |
| checkout-repo | Perform checkout as first step of action | `false` | true |
| create-prerelease | Whether semantic-release should create a prerelease or do a dry run. This can be useful to set to true when a prerelease requires pushing artifacts semantic-release is in charge of generating | `false` | false |
| github-token | GitHub token that can checkout the repository as well as create tags/releases against it. e.g. 'secrets.GITHUB_TOKEN' | `true` |  |
| extra-plugins | Extra plugins for pre-install. You can also specify specifying version range for the extra plugins if you prefer. Defaults to install @open-turo/semantic-release-config. | `false` | @open-turo/semantic-release-config  |
| artifactory-username | Artifactory user name usually secrets.ARTIFACTORY_USERNAME | `true` |  |
| artifactory-auth-token | Artifactory auth token usually secrets.ARTIFACTORY_AUTH_TOKEN | `true` |  |
| gradle-cache-enabled | Whether to enable Gradle caching via gradle/actions/setup-gradle | `false` | true |
<!-- action-docs-inputs -->

<!-- action-docs-outputs -->
## Outputs

| parameter | description |
| --- | --- |
| new-release-published | Whether a new release was published |
| new-release-version | Version of the new release |
| new-release-major-version | Major version of the new release |
| pull-request-number | Pull request number |
| run-url | URL to the GHA run |
<!-- action-docs-outputs -->

<!-- action-docs-runs -->
## Runs

This action is a `composite` action.
<!-- action-docs-runs -->

<!-- action-docs-usage  -->
<!-- action-docs-usage -->
<!-- prettier-ignore-end -->

## Additional Examples

### using output parameters example

```yaml
jobs:
  build:
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: Release
        uses: open-turo/actions-jvm/prerelease@v1
        id: semantic # Need an `id` for output variables
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}

      - name: Do something when a new release published
        if: steps.semantic.outputs.new-release-published == 'true'
        run: |
          echo ${{ steps.semantic.outputs.new-release-version }}
          echo ${{ steps.semantic.outputs.new-release-major-version }}
```

## Notes

- By default, this action will perform actions/checkout as its first step.
- Unlike prerelease-msvc, this action doesn't include Docker functionality.
- This action uses [gradle/actions/setup-gradle](https://github.com/gradle/actions/blob/main/docs/setup-gradle.md) for Gradle dependency caching to improve build performance.
- Repositories using this action are expected to include a Gradle wrapper (`gradlew` and `gradle/wrapper/`) in their codebase.
