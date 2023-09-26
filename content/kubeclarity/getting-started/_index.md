---
title: Getting started
weight: 400
---

## KubeClarity Backend

### Prerequisites

KubeClarity requires these Kubernetes permissions:

| Permission | Reason |
| ---        | ---    |
| Read secrets in CREDS_SECRET_NAMESPACE (default: kubeclarity) | This allows you to configure image pull secrets for scanning private image repositories. |
| Read config maps in the KubeClarity deployment namespace. | This is required for getting the configured template of the scanner job. |
| List pods in cluster scope. | This is required for calculating the target pods that need to be scanned. |
| List namespaces. | This is required for fetching the target namespaces to scan in K8s runtime scan UI. |
| Create and delete jobs in cluster scope. | This is required for managing the jobs that scan the target pods in their namespaces. |

### Install using Helm

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

### Uninstall using Helm

1. Helm uninstall

   ```shell
   helm uninstall kubeclarity -n kubeclarity
   ```

2. Clean the resources. By default, Helm doesn't remove the PVCs and PVs for the StatefulSets. Run the following command to delete them all:

    ```shell
    kubectl delete pvc -l app.kubernetes.io/instance=kubeclarity -n kubeclarity
    ```

### Build and run locally with demo data

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

2. Open the KubeClarity UI in your browser: [http://localhost:8080/](http://localhost:8080/)

## CLI

KubeClarity includes a CLI that can be run locally and is especially useful for CI/CD pipelines.
It allows you to analyze images and directories to generate SBOM, and scan it for vulnerabilities.
The results can be exported to the KubeClarity backend.

### Installation

You can install the KubeClarity CLI using the following methods:

<details><summary>Binary Distribution</summary><p>

1. Download the release distribution for your OS from the [releases page](https://github.com/openclarity/kubeclarity/releases).
1. Unpack the `kubeclarity-cli` binary, then add it to your PATH.

</p></details>

<details><summary>Docker Image</summary><p>

A Docker image is available at `ghcr.io/openclarity/kubeclarity-cli` with list of
available tags [here](https://github.com/openclarity/kubeclarity/pkgs/container/kubeclarity-cli/versions).

</p></details>

<details><summary>Local Compilation</summary><p>

```
make cli
```

Copy `./cli/bin/cli` to your PATH under `kubeclarity-cli`.

</p></details>

### Generate SBOM

To generate the Software Bill of Materials (SBOM), run the following command:

```shell
kubeclarity-cli analyze <image/directory name> --input-type <dir|file|image(default)> -o <output file or stdout>
```

For example:

```shell
kubeclarity-cli analyze --input-type image nginx:latest -o nginx.sbom
```

You can list the content analyzers to use using the `ANALYZER_LIST` environment variable separated by a space (`ANALYZER_LIST="<analyzer 1 name> <analyzer 2 name>"`) For example:

```shell
ANALYZER_LIST="syft gomod" kubeclarity-cli analyze --input-type image nginx:latest -o nginx.sbom
```

### Vulnerability scanning

Usage:

```shell
kubeclarity-cli scan <image/sbom/directory/file name> --input-type <sbom|dir|file|image(default)> -f <output file>
```

Example:

```shell
kubeclarity-cli scan nginx.sbom --input-type sbom
```

You can list the vulnerability scanners to use using the `SCANNERS_LIST` environment variable separated by a space (`SCANNERS_LIST="<Scanner1 name> <Scanner2 name>"`)

For example:

```shell
SCANNERS_LIST="grype trivy" kubeclarity-cli scan nginx.sbom --input-type sbom
```

### Export results to KubeClarity backend

To export the CLI results to the KubeClarity backend, use an application ID as defined by the KubeClarity backend.
You can find the application ID on the **Applications** screen of the UI, or you can use the KubeClarity API.

#### Export SBOM

To export the SBOM to the KubeClarity backend, set the `BACKEND_HOST` environment variable and the `-e` flag.

> Note: Until TLS is supported, set `BACKEND_DISABLE_TLS=true`.

```shell
BACKEND_HOST=<KubeClarity backend address> BACKEND_DISABLE_TLS=true kubeclarity-cli analyze <image> --application-id <application ID> -e -o <SBOM output file>
```

For example:

```shell
BACKEND_HOST=localhost:9999 BACKEND_DISABLE_TLS=true kubeclarity-cli analyze nginx:latest --application-id 23452f9c-6e31-5845-bf53-6566b81a2906 -e -o nginx.sbom
```

#### Export vulnerability scan results

To export the vulnerability scan results to the KubeClarity backend, set the `BACKEND_HOST` environment variable and the `-e` flag.

> Note: Until TLS is supported, set `BACKEND_DISABLE_TLS=true`.

```shell
BACKEND_HOST=<KubeClarity backend address> BACKEND_DISABLE_TLS=true kubeclarity-cli scan <image> --application-id <application ID> -e
```

For example:

```shell
SCANNERS_LIST="grype" BACKEND_HOST=localhost:9999 BACKEND_DISABLE_TLS=true kubeclarity-cli scan nginx.sbom --input-type sbom  --application-id 23452f9c-6e31-5845-bf53-6566b81a2906 -e
```
