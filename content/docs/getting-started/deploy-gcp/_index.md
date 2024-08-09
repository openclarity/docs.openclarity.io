---
title: Deploy on GCP
weight: 110
---

## Prerequisites

* You can install OpenClarity using the CLI, so you have to have [gcloud](https://cloud.google.com/sdk/gcloud) on your
computer available beforehand. For details on installing and configuring gcloud, see the [official installation guide](https://cloud.google.com/sdk/docs/install).
* If you have already installed OpenClarity before and want to reinstall it, you have to manually [restore deleted roles](#restore-deleted-roles) that were created during the previous installation.

## Deployment steps

To install OpenClarity on [Google Cloud Platform (GCP)](https://cloud.google.com), complete the following steps.

1. Download the newest GCP deployment release from GitHub and extract it to any location.

    ```shell
    wget https://github.com/openclarity/openclarity/releases/download/v{{< param "latest_version" >}}/gcp-deployment-v{{< param "latest_version" >}}.tar.gz
    ```

1. Create a new directory, extract the files and navigate to the directory.

    ```shell
    mkdir gcp-deployment-v{{< param "latest_version" >}}
    tar -xvzf gcp-deployment-v{{< param "latest_version" >}}.tar.gz -C gcp-deployment-v{{< param "latest_version" >}}
    cd gcp-deployment-v{{< param "latest_version" >}}
    ```

1. Copy the example configuration file and rename it.

    ```shell
    cp vmclarity-config.example.yaml vmclarity-config.yaml
    ```

1. The following table contains all the fields that can be set in the `vmclarity-config.yaml` file. You have to set at
   least the required ones.

   | Field                           | Required | Default                                                                     | Description                                                                         |
   |---------------------------------|----------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
   | `zone`                          | **yes**  |                                                                             | The Zone to locate the OpenClarity server.                                            |
   | `machineType`                   | **yes**  |                                                                             | The machine type for the OpenClarity server.                                          |
   | `region`                        | **yes**  |                                                                             | The region to locate OpenClarity.                                                     |
   | `scannerMachineType`            |          | `e2-standard-2`                                                             | Machine type to use for the Scanner instances.                                      |
   | `scannerSourceImage`            |          | `projects/ubuntu-os-cloud/global/images/ubuntu-2204-jammy-v20230630`        | Source image to use for the Scanner instances.                                      |
   | `databaseToUse`                 |          | `SQLite`                                                                    | The database that OpenClarity should use.                                             |
   | `apiserverContainerImage`       |          | `ghcr.io/openclarity/vmclarity-apiserver:{{< param "latest_version" >}}`    | The container image to use for the apiserver.                                       |
   | `orchestratorContainerImage`    |          | `ghcr.io/openclarity/vmclarity-orchestrator:{{< param "latest_version" >}}` | The container image to use for the orchestrator.                                    |
   | `uiContainerImage`              |          | `ghcr.io/openclarity/vmclarity-ui:{{< param "latest_version" >}}`           | The container image to use for the ui.                                              |
   | `uibackendContainerImage`       |          | `ghcr.io/openclarity/vmclarity-ui-backend:{{< param "latest_version" >}}`   | The container image to use for the uibackend.                                       |
   | `scannerContainerImage`         |          | `ghcr.io/openclarity/vmclarity-cli:{{< param "latest_version" >}}`          | The container image to use for the scanner.                                         |
   | `exploitDBServerContainerImage` |          | `ghcr.io/openclarity/exploit-db-server:v0.2.4`                              | The container image to use for the exploit db server.                               |
   | `trivyServerContainerImage`     |          | `docker.io/aquasec/trivy:0.41.0`                                            | The container image to use for the trivy server.                                    |
   | `grypeServerContainerImage`     |          | `ghcr.io/openclarity/grype-server:v0.7.0`                                   | The container image to use for the grype server.                                    |
   | `freshclamMirrorContainerImage` |          | `ghcr.io/openclarity/freshclam-mirror:v0.2.0`                               | The container image to use for the fresh clam mirror server.                        |
   | `postgresqlContainerImage`      |          | `docker.io/bitnami/postgresql:12.14.0-debian-11-r28`                        | The container image to use for the postgresql server.                               |
   | `assetScanDeletePolicy`         |          | `Always`                                                                    | When asset scans should be cleaned up after scanning.                               |
   | `postgresDBPassword`            |          |                                                                             | Postgres DB password. Only required if DatabaseToUse is Postgresql.                 |
   | `externalDBName`                |          |                                                                             | DB to use in the external DB. Only required if DatabaseToUse is External.           |
   | `externalDBUsername`            |          |                                                                             | Username for the external DB. Only required if the DatabaseToUse is External.       |
   | `externalDBPassword`            |          |                                                                             | Password for the external DB. Only required if the DatabaseToUse is External.       |
   | `externalDBHost`                |          |                                                                             | Hostname or IP for the external DB. Only required if the DatabaseToUse is External. |
   | `externalDBPort`                |          |                                                                             | Port for the external DB. Only required if the DatabaseToUse is External.           |

1. Deploy OpenClarity using gcloud deployment-manager.

   ```shell
   gcloud deployment-manager deployments create <vmclarity deployment name> --config vmclarity-config.yaml
   ```

1. Open an SSH tunnel to the OpenClarity server with gcloud. For further information on how to create an SSH connection
   with gcloud to one of your instances check the [official page](https://cloud.google.com/compute/docs/connect/standard-ssh#gcloud).

   ```shell
   gcloud compute ssh --project=<project id> --zone=<zone name> <name of your VM> -- -NL 8080:localhost:80
   ```

1. Access the OpenClarity UI.

    {{< include-headless "vmclarity/access-ui.md" >}}

## Next steps

Complete the {{% xref "/docs/getting-started/first-tasks/_index.md" %}}.

## Uninstall OpenClarity

1. You can uninstall OpenClarity using the gcloud manager.

   ```shell
   gcloud deployment-manager deployments delete <vmclarity deployment name>
   ```

## Restore deleted roles

1. On the [IAM & Admin page](https://console.cloud.google.com/iam-admin/roles) on GCP, open the **Roles tab**, then search for OpenClarity in the filter input.

1. Now manually undelete the Discoverer Snapshotter and Scanner roles to set their statuses from Deleted to Enabled.

   ![Undelete roles](/img/vmclarity-gcp-undelete-roles.png)
