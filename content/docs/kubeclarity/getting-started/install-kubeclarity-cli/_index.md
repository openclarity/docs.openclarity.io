---
title: Install the CLI
weight: 200
---

Kubernetes Security includes a CLI that can be run locally and is especially useful for CI/CD pipelines. It allows you to analyze images and directories to generate SBOM, and scan it for vulnerabilities. The results can be exported to the Kubernetes Security backend.

You can install the Kubernetes Security CLI using the following methods:

<details><summary>Binary Distribution</summary><p>

1. Download the release distribution for your OS from the [releases page](https://github.com/openclarity/kubeclarity/releases).
1. Unpack the `kubeclarity-cli` binary, then add it to your PATH.

</p></details>

<details><summary>Docker Image</summary><p>

A Docker image is available at `ghcr.io/openclarity/kubeclarity-cli` with list of
available tags [here](https://github.com/openclarity/kubeclarity/pkgs/container/kubeclarity-cli/versions).

</p></details>

<details><summary>Local Compilation</summary><p>

1. [Clone the project repo](https://github.com/openclarity/kubeclarity/).
1. Run:

    ```shell
    make cli
    ```

1. Copy `./cli/bin/cli` to your PATH under `kubeclarity-cli`.

</p></details>

## Next step

Check the common tasks you can do using the [web UI]({{< relref "/docs/kubeclarity/getting-started/first-tasks-ui/_index.md" >}}).
