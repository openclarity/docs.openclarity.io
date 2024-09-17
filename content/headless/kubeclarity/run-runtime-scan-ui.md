---
---
To start a [runtime scan]({{< relref "/docs/features/kubernetes_scanning.md" >}}), complete the following steps.

1. {{< include-headless "kubeclarity/open-ui.md" >}}
1. From the navigation bar on the left, select **Runtime Scan**.

    ![Select runtime scan](/docs/kubeclarity/getting-started/first-tasks-ui/run-time-scan.png)

1. Select the namespace you want to scan, for example, the `sock-shop` namespace if you have installed the demo application, then click **START SCAN**. You can select multiple namespaces.

    ![Start a runtime scan on a namespace](/docs/kubeclarity/getting-started/first-tasks-ui/start-run-time-scan.png)

1. Wait until the scan is completed, then check the results. The scan results report the affected components such as **Applications**, **Application Resources**, **Packages**, and **Vulnerabilities**.

    ![Scan results](/docs/kubeclarity/getting-started/first-tasks-ui/run-time-scan-results.png)

1. Click on these elements for details. For example, **Applications** shows the applications in the namespace that have vulnerabilities detected.

    ![Scan results details](/docs/kubeclarity/getting-started/first-tasks-ui/run-time-scan-results-details.png)

1. Now that you have run a scan, a summary of the results also appears on the dashboard page of the UI.

    ![Dashboard with data](/docs/kubeclarity/getting-started/first-tasks-ui/dashboard-with-data.png)
