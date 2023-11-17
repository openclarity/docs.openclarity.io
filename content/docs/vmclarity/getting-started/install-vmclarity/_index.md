---
title: Install VMClarity
weight: 100
---

Install the VMClarity backend on the platform of your choice.

- [AWS]({{< relref "/docs/vmclarity/getting-started/deploy-aws/_index.md" >}})
- [Azure](#azure)
- [GCP]({{< relref "/docs/vmclarity/getting-started/gcp/_index.md" >}})
- [Docker]({{< relref "/docs/vmclarity/getting-started/deploy-docker/_index.md" >}})

## Azure

1. Click the [![Deploy To Azure](https://docs.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fvmclarity%2Fazure_installer%2Finstallation%2Fazure%2Fvmclarity.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fvmclarity%2Fazure_installer%2Finstallation%2Fazure%2Fvmclarity-UI.json) button.
2. Fill out the required fields in the wizard
3. Once deployed, copy the VMClarity SSH address from the Outputs tab
1. [Open the VMClarity UI](#access-ui).

## Access VMClarity UI {#access-ui}

{{< include-headless "vmclarity/access-ui.md" >}}

Complete the {{% xref "/docs/vmclarity/getting-started/first-tasks/_index.md" %}}.
