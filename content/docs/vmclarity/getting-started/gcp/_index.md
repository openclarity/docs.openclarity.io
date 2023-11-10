---
title: Installing on GCP
weight: 300
---

These instructions are for installing VMClarity on [GCP (Google Cloud Platform)](https://cloud.google.com).

### Prerequisites

VMClarity on GCP can be installed currently via the CLI, so you have to have
[gcloud](https://cloud.google.com/sdk/gcloud) on your computer available beforehand. For further instructions about
installing and configuring gcloud check the [official installation guide](https://cloud.google.com/sdk/docs/install).

### Installation instructions

1. Download the newest GCP deployment release from GitHub and extract it to any location.

    ```shell
    curl -sSfL https://github.com/openclarity/vmclarity/releases/download/v0.6.0/gcp-deployment-v0.6.0.tar.gz --output - | tar -xzvf -
    ```

2. Change into the extracted directory.

    ```shell
    cd gcp-deployment-v0.6.0
    ```

3. Copy the example configuration file and rename it.

    ```shell
    cp vmclarity-config.example.yaml vmclarity-config.yaml
    ```

4. The following table contains all the fields that can be set in the `vmclarity-config.yaml` file. You have to set at
   least the required ones.

   | Field                           | Required | Default                                                              | Description                                                                         |
   |---------------------------------|----------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------|
   | `zone`                          | **yes**  |                                                                      | The Zone to locate the VMClarity server.                                            |
   | `machineType`                   | **yes**  |                                                                      | The machine type for the VMClarity server.                                          |
   | `region`                        | **yes**  |                                                                      | The region to locate VMClarity.                                                     |
   | `scannerMachineType`            |          | `e2-standard-2`                                                      | Machine type to use for the Scanner instances.                                      |
   | `scannerSourceImage`            |          | `projects/ubuntu-os-cloud/global/images/ubuntu-2204-jammy-v20230630` | Source image to use for the Scanner instances.                                      |
   | `databaseToUse`                 |          | `SQLite`                                                             | The database that VMClarity should use.                                             |
   | `apiserverContainerImage`       |          | `ghcr.io/openclarity/vmclarity-apiserver:latest`                     | The container image to use for the apiserver.                                       |
   | `orchestratorContainerImage`    |          | `ghcr.io/openclarity/vmclarity-orchestrator:latest`                  | The container image to use for the orchestrator.                                    |
   | `uiContainerImage`              |          | `ghcr.io/openclarity/vmclarity-ui:latest`                            | The container image to use for the ui.                                              |
   | `uibackendContainerImage`       |          | `ghcr.io/openclarity/vmclarity-ui-backend:latest`                    | The container image to use for the uibackend.                                       |
   | `scannerContainerImage`         |          | `ghcr.io/openclarity/vmclarity-cli:latest`                           | The container image to use for the scanner.                                         |
   | `exploitDBServerContainerImage` |          | `ghcr.io/openclarity/exploit-db-server:v0.2.4`                       | The container image to use for the exploit db server.                               |
   | `trivyServerContainerImage`     |          | `docker.io/aquasec/trivy:0.41.0`                                     | The container image to use for the trivy server.                                    |
   | `grypeServerContainerImage`     |          | `ghcr.io/openclarity/grype-server:v0.7.0`                            | The container image to use for the grype server.                                    |
   | `freshclamMirrorContainerImage` |          | `ghcr.io/openclarity/freshclam-mirror:v0.2.0`                        | The container image to use for the fresh clam mirror server.                        |
   | `postgresqlContainerImage`      |          | `docker.io/bitnami/postgresql:12.14.0-debian-11-r28`                 | The container image to use for the postgresql server.                               |
   | `assetScanDeletePolicy`         |          | `Always`                                                             | When asset scans should be cleaned up after scanning.                               |
   | `postgresDBPassword`            |          |                                                                      | Postgres DB password. Only required if DatabaseToUse is Postgresql.                 |
   | `externalDBName`                |          |                                                                      | DB to use in the external DB. Only required if DatabaseToUse is External.           |
   | `externalDBUsername`            |          |                                                                      | Username for the external DB. Only required if the DatabaseToUse is External.       |
   | `externalDBPassword`            |          |                                                                      | Password for the external DB. Only required if the DatabaseToUse is External.       |
   | `externalDBHost`                |          |                                                                      | Hostname or IP for the external DB. Only required if the DatabaseToUse is External. |
   | `externalDBPort`                |          |                                                                      | Port for the external DB. Only required if the DatabaseToUse is External.           |

5. Deploy VMClarity using gcloud deployment-manager.

   ```shell
   gcloud deployment-manager deployments create <vmclarity deployment name> --config vmclarity-config.yaml
   ```

### Access VMClarity UI

1. Open an SSH tunnel to the VMClarity server with gcloud. For further information on how to create an SSH connection
   with gcloud to one of your instances check the [official page](https://cloud.google.com/compute/docs/connect/standard-ssh#gcloud).

   ```shell
   gcloud compute ssh --project=<project id> --zone=<zone name> <name of you VM> -- -NL 8080:localhost:80
   ```

2. Open the VMClarity UI in your browser at [http://localhost:8080](http://localhost:8080).

   ![VMClarity UI Dashboard](/img/vmclarity-ui-1.png)

3. (Optional) If needed, you can access the API at [http://localhost:8080/api](http://localhost:8080/api). For details on the API, see {{% xref "/docs/vmclarity/api/_index.md" %}}.
