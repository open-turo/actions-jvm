# GitHub Action Release

GitHub Action for [Semantic Release][semantic-url].

## Usage

Note: by default, this action will perform actions/checkout as its first step.

### Step1: Set any [Semantic Release Configuration](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#configuration) in your repository.

### Step2: [Add Secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) in your repository for the [Semantic Release Authentication](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/ci-configuration.md#authentication) Environment Variables.

### Step3: Add a [Workflow File](https://help.github.com/en/articles/workflow-syntax-for-github-actions) to your repository to create custom automated processes.

#### Basic Usage:

```yaml
steps:
  - name: Action semantic release
    uses: open-turo/actions-jvm/release@v1
    with:
      github-token: ${{ secrets.GITHUB_TOKEN }}
```

**IMPORTANT**: `GITHUB_TOKEN` does not have the required permissions to operate on protected branches.
If you are using this action for protected branches, replace `GITHUB_TOKEN` with [Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line). If using the `@semantic-release/git` plugin for protected branches, avoid persisting credentials as part of `actions/checkout@v2` by setting the parameter `persist-credentials: false`. This credential does not have the required permission to operate on protected branches.

### Inputs

| Input Parameter | Required | Description                                                                                                           |
| :-------------: | :------: | --------------------------------------------------------------------------------------------------------------------- |
|  checkout-repo  |  false   | Whether or not to checkout the repo as the first step                                                                 |
|  github-token   |   true   | GitHub token that can checkout the repository as well as create tags/releases against it. e.g. 'secrets.GITHUB_TOKEN' |
|   go-version    |  false   | The version of golang that is needed                                                                                  |

### Outputs

|     Output Parameter      | Description                                                                                                                       |
| :-----------------------: | --------------------------------------------------------------------------------------------------------------------------------- |
|   new-release-published   | Whether a new release was published (`true` or `false`)                                                                           |
|    new-release-version    | Version of the new release. (e.g. `1.3.0`)                                                                                        |
| new-release-major-version | Major version of the new release. (e.g. `1`)                                                                                      |
|    new-release-channel    | The distribution channel on which the last release was initially made available (undefined for the default distribution channel). |

#### Using Output Variables:

```yaml
jobs:
  build:
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Semantic release
        uses: open-turo/actions-jvm/release@v1
        id: semantic # Need an `id` for output variables
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}

      - name: Do something when a new release published
        if: steps.release.outputs.new-release-published == 'true'
        run: |
          echo ${{ steps.semantic.outputs.new-release-version }}
          echo ${{ steps.semantic.outputs.new-release-major-version }}
```
