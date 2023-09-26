---
title: Trivy
weight: 100
---

The Trivy scanner supports remote mode using the Trivy server. The trivy server can be deployed as documented here: [trivy client-server mode](https://aquasecurity.github.io/trivy/v0.34/docs/references/modes/client-server/).

Instructions to install the Trivy CLI are available here: [trivy install](https://aquasecurity.github.io/trivy/v0.34/getting-started/installation/).

The Aqua team provides an official container image that can be used to run the server in Kubernetes or docker, which we'll use in the examples.

1. Start the server:

    ```shell
    docker run -p 8080:8080 --rm aquasec/trivy:0.41.0 server --listen 0.0.0.0:8080
    ```

1. Run a scan using the server:

    ```shell
    SCANNERS_LIST="trivy" SCANNER_TRIVY_SERVER_ADDRESS="http://<trivy server address>:8080" ./kubeclarity_cli scan --input-type sbom nginx.sbom
    ```

## Authentication

The trivy server also provides token based authentication to prevent unauthorized use of a trivy server instance. You can enable it by running the server with `--token` flag:

```shell
docker run -p 8080:8080 --rm aquasec/trivy:0.41.0 server --listen 0.0.0.0:8080 --token mytoken
```

Then pass the token to the scanner:

```shell
SCANNERS_LIST="trivy" SCANNER_TRIVY_SERVER_ADDRESS="http://<trivy server address>:8080" SCANNER_TRIVY_SERVER_TOKEN="mytoken" ./kubeclarity_cli scan --input-type sbom nginx.sbom
```
