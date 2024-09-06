---
title: Deploy on Docker
weight: 110
---

## Prerequisites

* Install [Docker](https://docs.docker.com/get-docker/).

## Deployment steps

To run VMClarity in Docker on a local machine, complete the following steps.

1. Download the latest VMClarity release.

    ```shell
    wget https://github.com/openclarity/vmclarity/releases/download/v{{< param "latest_version" >}}/docker-compose-v{{< param "latest_version" >}}.tar.gz
    ```

1. Create a new directory, extract the files and navigate to the directory.

    ```shell
    mkdir docker-compose-v{{< param "latest_version" >}}
    tar -xvzf docker-compose-v{{< param "latest_version" >}}.tar.gz -C docker-compose-v{{< param "latest_version" >}}
    cd docker-compose-v{{< param "latest_version" >}}
    ```

1. Start every control plane element with the docker compose file.

    ```shell
    docker compose --project-name vmclarity --file docker-compose.yml up -d --wait --remove-orphans
    ```

    The output should be similar to:

    ```
    [+] Running 14/14
    ⠿ Network vmclarity                        Created                                                       0.2s
    ⠿ Volume "vmclarity_grype-server-db"       Created                                                       0.0s
    ⠿ Volume "vmclarity_apiserver-db-data"     Created                                                       0.0s
    ⠿ Container vmclarity-orchestrator-1       Healthy                                                      69.7s
    ⠿ Container vmclarity-yara-rule-server-1   Healthy                                                      17.6s
    ⠿ Container vmclarity-exploit-db-server-1  Healthy                                                      17.7s
    ⠿ Container vmclarity-swagger-ui-1         Healthy                                                       7.8s
    ⠿ Container vmclarity-trivy-server-1       Healthy                                                      26.7s
    ⠿ Container vmclarity-uibackend-1          Healthy                                                      17.6s
    ⠿ Container vmclarity-ui-1                 Healthy                                                       7.7s
    ⠿ Container vmclarity-freshclam-mirror-1   Healthy                                                       7.8s
    ⠿ Container vmclarity-grype-server-1       Healthy                                                      37.3s
    ⠿ Container vmclarity-gateway-1            Healthy                                                       7.7s
    ⠿ Container vmclarity-apiserver-1          Healthy                                                      17.7s
    ```

    Please note that the `image_override.env` file enables you to use the images you build yourself. You can override parameters in the `docker-compose.yml` by passing a custom env file to the `docker compose up` command via the `--env-file` flag. The `/installation/docker/image_override.env` file contains an example overriding all the container images.

1. Check the running containers in the Docker desktop.

    <p align="center" width="100%">
        <img width="75%" src="vmclarity-docker.png">
    </p>

1. Access the VMClarity UI. Navigate to [http://localhost:8080/](http://localhost:8080/) in your browser.

    <p align="center" width="100%">
        <img width="75%" src="/img/archive-vmclarity-ui-1.png">
    </p>

## Next steps

Complete the {{% xref "/docs/archive/vmclarity/getting-started/first-tasks/_index.md" %}}.

## Clean up steps

1. After you've finished your tasks, stop the running containers.

    ```shell
    docker compose --project-name vmclarity --file docker-compose.yml down --remove-orphans
    ```
