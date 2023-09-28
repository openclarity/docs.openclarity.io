---
title: Install the KubeClarity backend
linktitle: Install the backend
weight: 100
---

You can install the KubeClarity backend using [Helm](#install-using-helm), or you can [build and run it locally](#build-locally).

## Prerequisites

KubeClarity requires these Kubernetes permissions:

| Permission | Reason |
| ---        | ---    |
| Read secrets in CREDS_SECRET_NAMESPACE (default: kubeclarity) | This allows you to configure image pull secrets for scanning private image repositories. |
| Read config maps in the KubeClarity deployment namespace. | This is required for getting the configured template of the scanner job. |
| List pods in cluster scope. | This is required for calculating the target pods that need to be scanned. |
| List namespaces. | This is required for fetching the target namespaces to scan in K8s runtime scan UI. |
| Create and delete jobs in cluster scope. | This is required for managing the jobs that scan the target pods in their namespaces. |

## Install using Helm

1. Add the Helm repository.

    ```shell
    helm repo add kubeclarity https://openclarity.github.io/kubeclarity
    ```

1. Save the default KubeClarity chart values.

    ```shell
    helm show values kubeclarity/kubeclarity > values.yaml
    ```

1. Check the configuration in the `values.yaml` file and update the required values if needed.

    - To enable and configure the supported SBOM generators and vulnerability scanners, check the `analyzer` and `scanner` configurations under the `vulnerability-scanner` section.

1. Deploy KubeClarity with Helm.

   ```shell
   helm install --values values.yaml --create-namespace kubeclarity kubeclarity/kubeclarity -n kubeclarity
   ```

   Alternatively, for an OpenShift Restricted SCC compatible installation, run:

   ```shell
   helm install --values values.yaml --create-namespace kubeclarity kubeclarity/kubeclarity -n kubeclarity --set global.openShiftRestricted=true \
     --set kubeclarity-postgresql.securityContext.enabled=false --set kubeclarity-postgresql.containerSecurityContext.enabled=false \
     --set kubeclarity-postgresql.volumePermissions.enabled=true --set kubeclarity-postgresql.volumePermissions.securityContext.runAsUser="auto" \
     --set kubeclarity-postgresql.shmVolume.chmod.enabled=false
   ```

1. Port-forward to the KubeClarity UI.

   ```shell
   kubectl port-forward -n kubeclarity svc/kubeclarity-kubeclarity 9999:8080
   ```

1. Open the KubeClarity UI in your browser at [http://localhost:9999/](http://localhost:9999/)
1. {{% xref "/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" %}}.

## Uninstall using Helm

Later if you have finished experimenting with KubeClarity, you can delete the backend by completing the following steps.

1. Helm uninstall

   ```shell
   helm uninstall kubeclarity -n kubeclarity
   ```

2. Clean the resources. By default, Helm doesn't remove the PVCs and PVs for the StatefulSets. Run the following command to delete them all:

    ```shell
    kubectl delete pvc -l app.kubernetes.io/instance=kubeclarity -n kubeclarity
    ```

## Build and run locally with demo data {#build-locally}

1. Build the UI and the backend and start the backend locally, either using Docker, or without it:

    - Using docker:
        1. Build UI and backend (the image tag is set using VERSION):

            ```shell
            VERSION=test make docker-backend
            ```

        1. Run the backend using demo data:

            ```shell
            docker run -p 8080:8080 -e FAKE_RUNTIME_SCANNER=true -e FAKE_DATA=true -e ENABLE_DB_INFO_LOGS=true -e DATABASE_DRIVER=LOCAL ghcr.io/openclarity/kubeclarity:test run
            ```

    - Local build:
        1. Build UI and backend

            ```shell
            make ui && make backend
            ```

        1. Copy the built site:

            ```shell
            cp -r ./ui/build ./site
            ```

        1. Run the backend locally using demo data:

            ```shell
            FAKE_RUNTIME_SCANNER=true DATABASE_DRIVER=LOCAL FAKE_DATA=true ENABLE_DB_INFO_LOGS=true ./backend/bin/backend run
            ```

1. Open the KubeClarity UI in your browser: [http://localhost:8080/](http://localhost:8080/)
1. {{% xref "/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" %}}.
