---
title: First tasks - CLI
weight: 400
---

After you have [installed the Kubernetes Security backend]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-backend/_index.md" >}}) and the [Kubernetes Security CLI]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" >}}), and completed the [first tasks on the UI]({{< relref "/docs/kubeclarity/getting-started/first-tasks-ui/_index.md" >}}), complete the following tasks to see the basic functionality of the Kubernetes Security CLI.

## Generate SBOM

{{< include-headless "kubeclarity/generate-sbom-simple-cli.md" >}}

## Vulnerability scan

{{< include-headless "kubeclarity/run-vulnerability-scan-cli.md" >}}

## Export results to Kubernetes Security backend

To export the CLI results to the Kubernetes Security backend, complete the following steps.

1. {{< include-headless "kubeclarity/get-application-id.md" >}}
1. {{< include-headless "kubeclarity/export-sbom-scan-results.md" >}}
1. {{< include-headless "kubeclarity/export-vulnerability-scan-results.md" >}}
1. Now you can [see the exported results on the UI]({{< relref "/docs/kubeclarity/getting-started/first-tasks-ui/_index.md#vulnerability-scan-results-ui" >}}), for example, on the **Dashboard** page.

## Next step

Now that you have finished the getting started guide, explore the UI, or check the documentation for other use cases.
