---
title: Grype
weight: 200
---

Grype supports remote mode using [grype-server](https://github.com/portshift/grype-server), a RESTful grype wrapper which provides an API that receives an SBOM and returns the grype scan results for that SBOM. Grype-server ships as a container image, so can be run in Kubernetes or via Docker standalone.

1. Start the server:

    ```shell
    docker run -p 9991:9991 --rm gcr.io/eticloud/k8sec/grype-server:v0.1.5
    ```

1. Run a scan using the server:

    ```shell
    SCANNERS_LIST="grype" SCANNER_GRYPE_MODE="remote" SCANNER_REMOTE_GRYPE_SERVER_ADDRESS="<grype server address>:9991" SCANNER_REMOTE_GRYPE_SERVER_SCHEMES="https" ./kubeclarity_cli scan --input-type sbom nginx.sbom
    ```

If the grype server is deployed with TLS, you can override the default URL scheme like this:

```shell
SCANNERS_LIST="grype" SCANNER_GRYPE_MODE="remote" SCANNER_REMOTE_GRYPE_SERVER_ADDRESS="<grype server address>:9991" SCANNER_REMOTE_GRYPE_SERVER_SCHEMES="https" ./kubeclarity_cli scan --input-type sbom nginx.sbom
```
