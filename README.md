# `open-turo/actions-jvm`

GitHub Actions for JVM based repositories using Gradle, such as for Java and Kotlin projects.

[![Release](https://img.shields.io/github/v/release/open-turo/actions-jvm)](https://github.com/open-turo/actions-jvm/releases/)
[![Tests pass/fail](https://img.shields.io/github/workflow/status/open-turo/actions-jvm/CI)](https://github.com/open-turo/actions-jvm/actions/)
[![License](https://img.shields.io/github/license/open-turo/actions-jvm)](./LICENSE)
[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](https://github.com/dwyl/esta/issues)
![CI](https://github.com/open-turo/actions-jvm/actions/workflows/release.yaml/badge.svg)
[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)
[![Conventional commits](https://img.shields.io/badge/conventional%20commits-1.0.2-%23FE5196?logo=conventionalcommits&logoColor=white)](https://conventionalcommits.org)
[![Join us!](https://img.shields.io/badge/Turo-Join%20us%21-593CFB.svg)](https://turo.com/jobs)

## Requirements

These actions are designed for JVM repositories that use **Gradle** as their build tool. Your repository should include:

- A Gradle wrapper (`gradlew` and `gradle/wrapper/` directory)
- Standard Gradle project structure

## Features

- **Gradle Caching**: Actions automatically leverage [gradle/actions/setup-gradle](https://github.com/gradle/actions/blob/main/docs/setup-gradle.md) to cache Gradle dependencies and build outputs, significantly improving workflow performance
- **Configurable Caching**: All actions include a `gradle-cache-enabled` input (defaults to `true`) to allow fine-grained control over caching behavior
- **Gradle Wrapper Support**: Works seamlessly with your project's included Gradle wrapper

## Actions

### action: [`lint`](./lint)

See usage [here](./lint/README.md#usage).

Documentation is found [here](./lint/README.md).

### action: [`release`](./release)

See usage [here](./release/README.md#usage).

Documentation is found [here](./release/README.md).

### action: [`test`](./test)

See usage [here](./test/README.md#usage).

Documentation is found [here](./test/README.md).

### action: [`prerelease`](./prerelease)

See usage [here](./prerelease/README.md#usage).

Documentation is found [here](./prerelease/README.md).

### action: [`prerelease-msvc`](./prerelease-msvc)

See usage [here](./prerelease-msvc/README.md#usage).

Documentation is found [here](./prerelease-msvc/README.md).

### action: [`build-docker`](./build-docker)

See usage [here](./build-docker/README.md#usage).

Documentation is found [here](./build-docker/README.md).

## Get Help

Each Action has a detailed README for how to use it as referenced above. Please review Issues, post new Issues against this repository as needed.

## Contributions

Please see [here](https://github.com/open-turo/contributions) for guidelines on how to contribute to this project.
