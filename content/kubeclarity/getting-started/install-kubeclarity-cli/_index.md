---
title: Install the CLI
weight: 200
---

KubeClarity includes a CLI that can be run locally and is especially useful for CI/CD pipelines. It allows you to analyze images and directories to generate SBOM, and scan it for vulnerabilities. The results can be exported to the KubeClarity backend.

You can install the KubeClarity CLI using the following methods:

<details><summary>Binary Distribution</summary><p>

1. Download the release distribution for your OS from the [releases page](https://github.com/openclarity/kubeclarity/releases).
1. Unpack the `kubeclarity-cli` binary, then add it to your PATH.

</p></details>

<details><summary>Docker Image</summary><p>

A Docker image is available at `ghcr.io/openclarity/kubeclarity-cli` with list of
available tags [here](https://github.com/openclarity/kubeclarity/pkgs/container/kubeclarity-cli/versions).

</p></details>

<details><summary>Local Compilation</summary><p>

1. Clone the project repo.
1. Run:

    ```shell
    make cli
    ```

1. Copy `./cli/bin/cli` to your PATH under `kubeclarity-cli`.

</p></details>

After you have installed the CLI, complete the [first tasks]({{< relref "/kubeclarity/getting-started/first-tasks/_index.md" >}}).
