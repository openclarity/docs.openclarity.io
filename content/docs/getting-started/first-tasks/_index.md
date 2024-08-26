---
title: First Tasks on the UI
weight: 200
---

## Configure your first scan

1. Open the UI.

   {{< include-headless "vmclarity/access-ui.md" >}}

2. Click on the **Scans** icon. In the Scans window, you can create a new scan configuration.

    <img src="/img/openclarity-ui-2.png" alt="OpenClarity UI Scan" title="OpenClarity UI Scan" />

3. Click **New scan configuration**.

    <img src="/img/openclarity-scan-setup-1.png" alt="OpenClarity Scan Setup - Step 1" title="OpenClarity Scan Setup Step 1" />

4. Follow the steps of the **New scan config** wizard to name the scan, and optionally narrow the scope down with an
   OData query.

    <img src="/img/openclarity-scan-setup-2.png" alt="OpenClarity Scan Setup - Step 2" title="OpenClarity Scan Setup Step 2" />

5. Enable the scan types you want to perform.

    <img src="/img/openclarity-scan-setup-3.png" alt="OpenClarity Scan Setup - Step 3" title="OpenClarity Scan Setup Step 3" />

6. Select the time and/or frequency of the scans. To run the scan immediately, select **Now**.

    <img src="/img/openclarity-scan-setup-4.png" alt="OpenClarity Scan Setup - Step 4" title="OpenClarity Scan Setup Step 4" />

7. Optionally, adjust the number of scanners to run in parallel and whether to use spot instances on cloud providers, or
   not.

    <img src="/img/openclarity-scan-setup-5.png" alt="OpenClarity Scan Setup - Step 5" title="OpenClarity Scan Setup Step 5" />

8. Click **Save**. The new scan appears on the **Scan Configurations** tab.

    <img src="/img/openclarity-scan-config-summary.png" alt="OpenClarity Scan Config Summary" title="OpenClarity Scan Config Summary" />

9. Once a scan is finished, you can browse around the various OpenClarity UI features and investigate the security scan reports.

   <img src="/img/openclarity-dashboard-data.png" alt="OpenClarity Dashboard with Findings" title="OpenClarity Dashboard with Findings" />
