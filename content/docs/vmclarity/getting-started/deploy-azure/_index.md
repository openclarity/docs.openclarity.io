---
title: Deploy on Azure
weight: 200
---

## Prerequisites

* Have an Azure subscription.
* Create a SSH public key for Linux. Please follow [these instructions for Linux and Mac users](https://learn.microsoft.com/en-gb/azure/virtual-machines/linux/mac-create-ssh-keys?WT.mc_id=Portal-fx) or [these for Windows users](https://learn.microsoft.com/en-gb/azure/virtual-machines/linux/ssh-from-windows). Once a RSA private key is created, convert it to a SSH2 public key with:

```sh
ssh-keygen -e -f ~/.ssh/id_rsa.pub > ~/.ssh/id_rsa2.pub
```

## Deployment steps

1. Click [here](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fvmclarity%2Fmain%2Finstallation%2Fazure%2Fvmclarity.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fvmclarity%2Fmain%2Finstallation%2Fazure%2Fvmclarity-UI.json) to deploy VMClarity's custom template.

2. Fill out the required project and instance details in the Basics tab.

<p align="center" width="100%">
    <img width="50%" src="azure-template-basics.png">
</p>

| Parameter                             | Required | Description                                                                                          |
|---------------------------------------|----------|------------------------------------------------------------------------------------------------------|
| Subscription                          | True     | Azure subscription where resources will be billed.                                                   |
| Region                                | False    | Azure region where resources will be deployed.                                                       |
| VMClarity Deploy Postfix              | True     | Postfix for Azure resource group name (e.g. `vmclarity-<postfix>`).                                  |
| VMClarity Server SSH Username         | True     | SSH Username for the VMClarity Server Virtual Machine.                                               |
| VMClarity Server SSH Public Key       | True     | SSH Public Key for the VMClarity Server Virtual Machine.                                             |
| VMClarity Server VM Size              | True     | The size of the VMClarity Server Virtual Machine.                                                    |
| VMClarity Scanner VMs Size            | True     | The size of the VMClarity Scanner Virtual Machines.                                                  |
| Security Type                         | False    | Security Type of the VMClarity Server Virtual Machine, e.g. `TrustedLaunch` (default) or `Standard`. |

3. In the Advanced tab, modify the Container Image for each service if a specific VMClarity version is required. Then, select the delete policy and the database.

<p align="center" width="100%">
    <img width="50%" src="azure-template-advanced.png">
</p>

| Parameter                             | Required | Description                                                                                               |
|---------------------------------------|----------|-----------------------------------------------------------------------------------------------------------|
| *Service* Container Image             | True     | Docker Container Image to use for each service.                                                           |
| Asset Scan Delete Policy              | True     | Delete Policy for resources created when performing an asset scan, e.g. `Always`, `OnSuccess` or `Never`. |
| Database To Use                       | True     | Database type to use, e.g. `SQLite`, `PostgreSQL` or `External PostgreSQL`.                               |

4. Review and create the deployment.

5. [TBC] Once the deployment is successful, copy the VMClarity SSH address from the Outputs tab.

<p align="center" width="100%">
    <img width="50%" src="azure-deploy-output.png">
</p>