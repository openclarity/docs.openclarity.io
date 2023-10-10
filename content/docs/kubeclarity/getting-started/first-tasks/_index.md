---
title: First tasks - CLI
weight: 300
---

After you have [installed the KubeClarity backend]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-backend/_index.md" >}}) and the [KubeClarity CLI]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" >}}), complete the following tasks to see the basic functionality of KubeClarity, either using the CLI, or using the [web UI]({{< relref "/docs/kubeclarity/getting-started/first-tasks-ui/_index.md" >}}).

## Generate SBOM

{{< include-headless "kubeclarity/generate-sbom-simple-cli.md" >}}

## Vulnerability scan

{{< include-headless "kubeclarity/run-vulnerability-scan-cli.md" >}}

## Export results to KubeClarity backend

To export the CLI results to the KubeClarity backend, complete the following steps.

1. {{< include-headless "kubeclarity/get-application-id.md" >}}
1. {{< include-headless "kubeclarity/export-sbom-scan-results.md" >}}
1. {{< include-headless "kubeclarity/export-vulnerability-scan-results.md" >}}
1. Now you can [see the exported results on the UI]({{< relref "/docs/kubeclarity/getting-started/first-tasks-ui/_index.md#vulnerability-scan-results-ui" >}}).
