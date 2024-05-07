# GitHub Action Release

<!-- prettier-ignore-start -->
<!-- action-docs-description -->
## Description

Builds and push docker images for the input platform, tags and image version
<!-- action-docs-description -->
<!-- prettier-ignore-end -->

## Usage

This action will build and publish a docker image with appropriate tags.

It assumes that the repo has a configuration file in `<repo-root>/.docker-config.json` with the following properties:

- `imageName`: the image name (org/image-name)
- `dockerfile`: the path to the dockerfile to build - defaults to `./Dockerfile`

Example:

```json
{
  "imageName": "turo/hello-world-msvc",
  "dockerfile": "./Dockerfile"
}
```

#### Basic Usage:

```yaml
steps:
  - uses: open-turo/actions-jvm/release@v3
    name: Release
    id: release
    with:
      checkout-repo: true
      github-token: ${{ secrets.GITHUB_TOKEN }}
      dry-run: false
  - uses: open-turo/actions-jvm/build-docker@v1
    id: docker-build
    with:
      dockerhub-user: ${{ secrets.DOCKER_USERNAME }}
      dockerhub-password: ${{ secrets.DOCKER_PASSWORD }}
      github-token: ${{ secrets.GITHUB_TOKEN }}
      artifactory-username: ${{ secrets.ARTIFACTORY_USERNAME }}
      artifactory-auth-token: ${{ secrets.ARTIFACTORY_AUTH_TOKEN }}
      image-version: ${{ steps.release.outputs.new-release-version }}
      docker-metadata-tags: |
        type=ref,event=branch
        type=ref,event=pr
        type=semver,pattern={{version}},value=${{ steps.release.outputs.new-release-version }}
```

**IMPORTANT** : `GITHUB_TOKEN` does not have the required permissions to operate on protected branches.
If you are using this action for protected branches, replace `GITHUB_TOKEN` with [Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line). If using the `@semantic-release/git` plugin for protected branches, avoid persisting credentials as part of `actions/checkout@v4` by setting the parameter `persist-credentials: false`. This credential does not have the required permission to operate on protected branches.

<!-- prettier-ignore-start -->
<!-- action-docs-inputs -->
## Inputs

| parameter | description | required | default |
| --- | --- | --- | --- |
| docker-config-file | Path to the docker config file (defaults to .docker-config.json) Must contain imageName, may contain dockerfile. | `false` | .docker-config.json |
| dockerhub-user | username for dockerhub | `true` |  |
| dockerhub-password | password for dockerhub | `true` |  |
| github-token | Usually secrets.GITHUB_TOKEN | `true` |  |
| artifactory-username | Artifactory user name usually secrets.ARTIFACTORY_USERNAME | `true` |  |
| artifactory-auth-token | Artifactory auth token usually secrets.ARTIFACTORY_AUTH_TOKEN | `true` |  |
| image-version | Docker image version | `true` |  |
| image-platform | Target platform to build image for (eg. linux/amd64 (default), linux/arm64, etc) | `false` | linux/amd64 |
| docker-metadata-tags | 'List of tags as key-value pair attributes' See: https://github.com/docker/metadata-action#tags-input | `false` |  |
<!-- action-docs-inputs -->

<!-- action-docs-outputs -->
## Outputs

| parameter | description |
| --- | --- |
| image-name | Docker image name |
| image-with-tag | Full image with tag - <image-name>:<image-version> |
<!-- action-docs-outputs -->

<!-- action-docs-runs -->
## Runs

This action is a `composite` action.
<!-- action-docs-runs -->

<!-- action-docs-usage  -->
<!-- action-docs-usage -->
<!-- prettier-ignore-end -->

#### Using Output Variables:

```yaml
steps:
  - uses: open-turo/actions-jvm/release@v3
    name: Release
    id: release
    with:
      checkout-repo: true
      github-token: ${{ secrets.GITHUB_TOKEN }}
      dry-run: false
  - uses: open-turo/actions-jvm/build-docker@v1
    id: docker-build
    with:
      dockerhub-user: ${{ secrets.DOCKER_USERNAME }}
      dockerhub-password: ${{ secrets.DOCKER_PASSWORD }}
      github-token: ${{ secrets.GITHUB_TOKEN }}
      artifactory-username: ${{ secrets.ARTIFACTORY_USERNAME }}
      artifactory-auth-token: ${{ secrets.ARTIFACTORY_AUTH_TOKEN }}
      image-version: ${{ steps.release.outputs.new-release-version }}
      image-platform: linux/arm64
      docker-metadata-tags: |
        type=ref,event=branch
        type=ref,event=pr
        type=semver,pattern={{version}},value=${{ steps.release.outputs.new-release-version }}
```
