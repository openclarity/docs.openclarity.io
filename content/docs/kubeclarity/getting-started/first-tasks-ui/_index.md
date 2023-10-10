---
title: First tasks - UI
weight: 400
---

After you have [installed the KubeClarity backend]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-backend/_index.md" >}}) and the [KubeClarity CLI]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" >}}), complete the following tasks to see the basic functionality of KubeClarity, either using the [CLI]({{< relref "/docs/kubeclarity/getting-started/first-tasks/_index.md" >}}), or using the web UI.

## Runtime scan

To start a [runtime scan]({{< relref "/docs/kubeclarity/concepts/runtime-scans/_index.md" >}}) from the UI, complete the following steps.

1. {{< include-headless "kubeclarity/open-ui.md" >}}
1. From the navigation bar on the left, select **Runtime Scan**.

    ![Select runtime scan](run-time-scan.png)

1. Select the namespace you want to scan, for example, the `sock-shop` namespace if you have installed the demo application, then click **START SCAN**. You can select multiple namespaces.

    ![Start a runtime scan on a namespace](start-run-time-scan.png)

1. Wait until the scan is completed, then check the results. The scan results report the affected components such as **Applications**, **Application Resources**, **Packages**, and **Vulnerabilities**.

    ![Scan results](run-time-scan-results.png)

1. Click on these elements for details. For example, **Applications** shows the applications in the namespace that have vulnerabilities detected.

    ![Scan results details](run-time-scan-results-details.png)

    Now that you have run a scan, a summary of the results also appears on the dashboard page of the UI.

    ![Dashboard with data](dashboard-with-data.png)

## Vulnerability scan {#vulnerability-scan-results-ui}

{{< include-headless "kubeclarity/vulnerability-scan-results-ui.md" >}}
