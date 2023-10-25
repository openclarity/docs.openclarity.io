---
title: Install VMClarity
weight: 100
---

Install the VMClarity backend on the platform of your choice.

## AWS

For a detailed installation guide, please see [AWS](https://github.com/openclarity/vmclarity/tree/main/installation/aws).

1. Start the CloudFormation [wizard](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=VMClarity&templateURL=https://s3.eu-west-2.amazonaws.com/vmclarity-v0.4.0/VmClarity.cfn), or upload the [latest](https://github.com/openclarity/vmclarity/releases/latest) CloudFormation template 
2. Specify the SSH key to be used to connect to VMClarity under 'KeyName'
3. Once deployed, copy VmClarity SSH Address from the "Outputs" tab
1. [Open the VMClarity UI](#access-ui).

## Azure

1. Click the [![Deploy To Azure](https://docs.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fvmclarity%2Fazure_installer%2Finstallation%2Fazure%2Fvmclarity.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fvmclarity%2Fazure_installer%2Finstallation%2Fazure%2Fvmclarity-UI.json) button.
2. Fill out the required fields in the wizard
3. Once deployed, copy the VMClarity SSH address from the Outputs tab
1. [Open the VMClarity UI](#access-ui).

## GCP

1. Change directory to `installation/gcp/dm`
2. Copy `vmclarity-config.example.yaml` to `vmclarity-config.yaml`, update with required values.
3. Deploy vmclarity using GCP deployment manager
   ```
   gcloud deployment-manager deployments create <vmclarity deployment name> --config vmclarity-config.yaml
   ```
4. Once deployed, copy the VMClarity SSH IP address from the CLI output.
1. [Open the VMClarity UI](#access-ui).

## Access VMClarity UI {#access-ui}

{{< include-headless "vmclarity/access-ui.md" >}}

Complete the {{% xref "/docs/vmclarity/getting-started/first-tasks/_index.md" %}}.
