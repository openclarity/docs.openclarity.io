---
title: Deploy on Azure
weight: 110
---

## Prerequisites

* Have an Azure subscription.
* Create an SSH public key for Linux. Please follow [these instructions for Linux and Mac users](https://learn.microsoft.com/en-gb/azure/virtual-machines/linux/mac-create-ssh-keys?WT.mc_id=Portal-fx) or [these for Windows users](https://learn.microsoft.com/en-gb/azure/virtual-machines/linux/ssh-from-windows). Once you have an RSA private key, convert it to an SSH2 public key with:

    ```sh
    ssh-keygen -e -f ~/.ssh/id_rsa.pub > ~/.ssh/id_rsa2.pub
    ```

## Deployment steps

1. Click [here](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fopenclarity%2Fmain%2Finstallation%2Fazure%2Fopenclarity.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fopenclarity%2Fopenclarity%2Fmain%2Finstallation%2Fazure%2Fopenclarity-UI.json) to deploy OpenClarity's custom template.

1. Fill out the required **Project details** and **Instance details** in the **Basics** tab.

    <p align="center" width="100%">
        <img width="75%" src="azure-template-basics.png">
    </p>

    You can set the following parameters:

    | Parameter                             | Required | Description                                                                                               |
    |---------------------------------------|----------|-----------------------------------------------------------------------------------------------------------|
    | Subscription                          | True     | Azure subscription where resources will be billed.                                                        |
    | Region                                | False    | Azure region where resources will be deployed.                                                            |
    | OpenClarity Deploy Postfix            | True     | Postfix for Azure resource group name (e.g. `openclarity-<postfix>`).                                       |
    | OpenClarity Server SSH Username       | True     | SSH Username for the OpenClarity Server Virtual Machine.                                                    |
    | OpenClarity Server SSH Public Key     | True     | SSH Public Key for the OpenClarity Server Virtual Machine. Paste the contents of `~/.ssh/id_rsa2.pub` here. |
    | OpenClarity Server VM Size            | True     | The size of the OpenClarity Server Virtual Machine.                                                         |
    | OpenClarity Scanner VMs Size          | True     | The size of the OpenClarity Scanner Virtual Machines.                                                       |
    | Security Type                         | False    | Security Type of the OpenClarity Server Virtual Machine, e.g. `TrustedLaunch` (default) or `Standard`.      |

1. (Optional) In the **Advanced** tab, modify the **Container Image** for each service if a specific OpenClarity version is required. Then, select the delete policy and the database.

    <p align="center" width="100%">
        <img width="75%" src="azure-template-advanced.png">
    </p>

    | Parameter                             | Required | Description                                                                                               |
    |---------------------------------------|----------|-----------------------------------------------------------------------------------------------------------|
    | *Service* Container Image             | True     | Docker Container Image to use for each service.                                                           |
    | Asset Scan Delete Policy              | True     | Delete Policy for resources created when performing an asset scan, e.g. `Always`, `OnSuccess` or `Never`. |
    | Database To Use                       | True     | Database type to use, e.g. `SQLite`, `PostgreSQL` or `External PostgreSQL`.                               |

1. Click **Review + create** to create the deployment.

1. Once the deployment is completed successfully, copy the OpenClarity SSH address from the **Outputs** tab.

    <p align="center" width="100%">
        <img width="75%" src="azure-deploy-output.png">
    </p>

1. {{< include-headless "vmclarity/ssh-tunnel-to-server.md" >}}

1. Access the OpenClarity UI.

    {{< include-headless "vmclarity/access-ui.md" >}}
 
## Next steps

Complete the {{% xref "/docs/getting-started/first-tasks/_index.md" %}}.
