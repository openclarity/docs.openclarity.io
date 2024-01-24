---
title: Deploy on AWS
weight: 110
---

An AWS CloudFormation template is provided for quick deployment of the VMClarity environment.

> Note: To avoid extra costs (cross-region snapshots), you may want to deploy the VMClarity AWS CloudFormation template in the same region where the majority of the VMs are that you want to scan with VMClarity.

The following figure shows the basic AWS resources that the VMClarity CloudFormation template creates:

- a VPC with a public and private subnet, and
- an AWS Internet Gateway (IGW) and NAT Gateway (NGW) into the VPC.

    <p align="center" width="100%">
        <img width="75%" src="vmclarity-cf-basic.svg">
    </p>

The public subnet (`VmClarityServerSubnet`) hosts the VMClarity Server (`VmClarityServer`) EC2 instance. The VMClarity server houses the scanning configuration, the UI, and other control components. The EC2 instance is assigned an external IPv4 address (EIP) for SSH and web UI access.

The private subnet (`VmClarityScannerSubnet`) hosts the VM snapshot instances (EC2) that are scanned for security vulnerabilities.

## Prerequisites

* Have an AWS account.
* Create an [EC2 key pair](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-keypair.html).

## Deployment steps

To deploy the VMClarity AWS CloudFormation Stack, you can:

- click [this quick-create link](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=VMClarity&templateURL=https://vmclarity-cfn.s3.eu-central-1.amazonaws.com/0.6.0/VmClarity.cfn) to navigate directly to the AWS CloudFormation console and jump to the wizard instructions, or 
- complete the following steps.

1. Download the latest VMClarity release.

    ```shell
    wget https://github.com/openclarity/vmclarity/releases/download/v{{< param "latest_version" >}}/aws-cloudformation-v{{< param "latest_version" >}}.tar.gz
    ```

    Alternatively, copy the [AWS CloudFormation template file](https://github.com/openclarity/vmclarity/blob/main/installation/aws/VmClarity.cfn) from the project repository to deploy the latest development code and skip the next step.

1. Create a new directory and extract the files.

    ```shell
    mkdir aws-cloudformation-v{{< param "latest_version" >}}
    tar -xvzf aws-cloudformation-v{{< param "latest_version" >}}.tar.gz -C aws-cloudformation-v{{< param "latest_version" >}}
    ```

1. Log in to the AWS CloudFormation console and go to the AWS CloudFormation Stacks section, then select **Create Stack > With New Resources (standard)**.

1. Check **Template is ready** and **Upload a template file**, then click **Upload a template file/Choose file** and upload the previously downloaded CFN template file.

    <p align="center" width="100%">
        <img width="100%" src="aws-cfn-template.png">
    </p>

1. In the VMClarity CloudFormation Stack wizard, set the following:

    1. Enter a name for the stack.
    1. Select the **InstanceType** (defaults to `t2.large` for the VMClarity Server, and the scanner VMs).
    1. Specify the SSH key for the EC2 instance in the **KeyName** field. You will need this key to connect to VMClarity.
    1. Adjust **SSHLocation** according to your policies.
    1. Do not change **AdvancedConfiguration**, unless you are building from a custom registry.
    1. Click **NEXT**.
    1. (Optional) Add tags as needed for your environment. You can use the defaults unless you need to adjust for your own policies.
    1. Click **NEXT**, then scroll to the bottom of the screen, and check **I acknowledge...**.
    1. Click **SUBMIT**.

1. Once the stack is deployed successfully, copy the VMClarity SSH address from the Outputs tab.

    <p align="center" width="100%">
        <img width="100%" src="aws-vmclarity-ssh.png">
    </p>

1. {{< include-headless "vmclarity/ssh-tunnel-to-server.md" >}}

1. Access the VMClarity UI.

    {{< include-headless "vmclarity/access-ui.md" >}}

## Next steps

Complete the {{% xref "/docs/vmclarity/getting-started/first-tasks/_index.md" %}}.
