---
title: First tasks on the UI
weight: 200
---

## Configure your first scan

1. Open the UI.

    {{< include-headless "vmclarity/access-ui.md" >}}

1. Click on the **Scans** icon. In the Scans window, you can create a new scan configuration.

    <img src="/img/vmclarity-ui-2.png" alt="VMClarity UI Scan" width="25%" height="25%" title="VMClarity UI Scan" />

1. Click **New scan configuration**.

    <img src="/img/vmclarity-scan-setup-1.png" alt="VMClarity Scan Setup - Step 1" width="40%" height="40%" title="VMClarity Scan Setup Step 1" />

1. Follow the steps of the **New scan config** wizard to name the scan, and identify the AWS scope (region, VPC, security groups, etc). The following example shows the AWS us-east-2 region, a specific VPC, and the `vmclarity-demo-vm` EC2

    <img src="/img/vmclarity-scan-setup-2.png" alt="VMClarity Scan Setup - Step 2" width="40%" height="40%" title="VMClarity Scan Setup Step 2" />

1. Enable the scan types you want to perform.

    <img src="/img/vmclarity-scan-setup-3.png" alt="VMClarity Scan Setup - Step 3" width="40%" height="40%" title="VMClarity Scan Setup Step 3" />

1. Select the time and/or frequency of the scans. To run the scan immediately, select **Now**.

    <img src="/img/vmclarity-scan-setup-4.png" alt="VMClarity Scan Setup - Step 4" width="40%" height="40%" title="VMClarity Scan Setup Step 4" />

1. Click **Save**. The new scan appears on the **Scan Configurations** tab.

    <img src="/img/vmclarity-scan-config-summary.png" alt="VMClarity Scan Config Summary" width="90%" height="90%" title="VMClarity Scan Config Summary" />

1. Once a scan is finished, you can browse around the various VMClarity UI features and investigate the security scan reports.

    <img src="/img/vmclarity-scan-list.png" alt="VMClarity Scan List" width="90%" height="90%" title="VMClarity Scan List" />

    <img src="/img/vmclarity-dashboard-data.png" alt="VMClarity Dashboard with Findings" width="90%" height="90%" title="VMClarity Dashboard with Findings" />
