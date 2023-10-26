---
title: Install VMClarity
weight: 100
---

Install the VMClarity backend on the platform of your choice.

- [AWS](#aws)
- [Azure](#azure)
- [GCP](#gcp)

## AWS

An AWS CloudFormation template is provided for quick deployment of the VMClarity environment.

> Note: To avoid extra costs (cross-region snapshots), you may want to deploy the VMClarity AWS CloudFormation template in the same region where the majority of the VMs are that you want to scan with VMClarity.

The following figure shows the basic AWS resources that the VMClarity CloudFormation template creates:

- a VPC with a public and private subnet, and
- an AWS Internet Gateway (IGW) and NAT Gateway (NGW) into the VPC.

![VMClarity CloudFormation resources](vmclarity-cf-basic.svg)

The public subnet (`VmClarityServerSubnet`) hosts the VMClarity Server (`VmClarityServer`) EC2 instance. The VMClarity server houses the scanning configuration, the UI, and other control components. The EC2 instance is assigned an external IPv4 address (EIP) for SSH and web UI access.

The private subnet (`VmClarityScannerSubnet`) hosts the VM snapshot instances (EC2) that are scanned for security vulnerabilities.

To deploy the VMClarity AWS CloudFormation Stack, complete the following steps.

1. Log in to the AWS CloudFormation console.

    - Click [here](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=VMClarity&templateURL=https://s3.eu-west-2.amazonaws.com/vmclarity-v{{< param "latest_version" >}}/VmClarity.cfn) to start the VMClarity CloudFormation Stack wizard.
    - Alternatively, you can:

        1. Download the latest stable VMClarity.cfn file from the [VMClarity releases page](https://github.com/openclarity/vmclarity/releases), or copy the AWS CloudFormation template file from the project repository to deploy the latest development code.
        1. Go to the AWS CloudFormation service page, then select **Create Stack > With New Resources (standard)**.
        1. Check **Template is ready** and **Upload a template file**, then click **Upload a template file/Choose file**.

1. In the VMClarity CloudFormation Stack wizard, set the following:

    1. Enter a name for the stack.
    1. Select the **InstanceType** (defaults to `t2.large` for the VMClarity Server, and the scanner VMs).
    1. Specify the SSH key for the EC2 instance in the **KeyName** field. You will need this key to connect to VMClarity.
    1. Adjust **SSHLocation** according to your policies.
    1. Do not change **AdvancedConfiguration**, unless you are building from a custom registry.
    1. Click **NEXT**.
    1. (Optional) Add tags as needed for your environment.  You can use the defaults unless you need to adjust for your own policies.
    1. Click **NEXT**, then scroll to the bottom of the screen, and check **I acknowledge...**.
    1. Click **SUBMIT**.

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
