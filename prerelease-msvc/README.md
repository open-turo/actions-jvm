# GitHub Action: Prerelease Microservice

## Description

GitHub Action to compute a prerelease version based on the latest release version and the number of commits since the
latest release. This will also generate a docker tag based on the computed version if the label `prerelease` is
specified on the PR.

## Configuration

### Step1: Set any [Semantic Release Configuration](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#configuration) in your repository.

### Step2: [Add Secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) in your repository for the [Semantic Release Authentication](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/ci-configuration.md#authentication) Environment Variables.

### Step3: Add a [Workflow File](https://help.github.com/en/articles/workflow-syntax-for-github-actions) to your repository to create custom automated processes.

## Usage

```yaml
steps:
  - name: Action semantic release
    uses: open-turo/actions-jvm/prerelease-msvc@v1
    with:
      github-token: ${{ secrets.GITHUB_TOKEN }}
```

**IMPORTANT**: `GITHUB_TOKEN` does not have the required permissions to operate on protected branches.
If you are using this action for protected branches, replace `GITHUB_TOKEN`
with [Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line).
If using the `@semantic-release/git` plugin for protected branches, avoid persisting credentials as part
of `actions/checkout@v4` by setting the parameter `persist-credentials: false`. This credential does not have the
required permission to operate on protected branches.

## Inputs

| parameter     | description                                                                                                           | required | default |
| ------------- | --------------------------------------------------------------------------------------------------------------------- | -------- | ------- |
| checkout-repo | Perform checkout as first step of action                                                                              | `false`  | true    |
| github-token  | GitHub token that can checkout the repository as well as create tags/releases against it. e.g. 'secrets.GITHUB_TOKEN' | `true`   |         |
| extra-plugins | Extra plugins for pre-install. You can also specify specifying version range for the extra plugins if you prefer.     | `false`  |         |

## Outputs

| parameter                 | description                         |
| ------------------------- | ----------------------------------- |
| new-release-published     | Whether a new release was published |
| new-release-version       | Version of the new release          |
| new-release-major-version | Major version of the new release    |

## Runs

This action is an `composite` action.

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
        uses: open-turo/actions-jvm/prerelease-msvc@v1
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