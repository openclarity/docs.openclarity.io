---
title: First tasks
weight: 300
---

After you have [installed the KubeClarity backend]({{< relref "/kubeclarity/getting-started/install-kubeclarity-backend/_index.md" >}}) and the [KubeClarity CLI]({{< relref "/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" >}}), complete the following tasks to see the basic functionality of KubeClarity.

## Generate SBOM

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

## Vulnerability scanning

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

## Export results to KubeClarity backend

To export the CLI results to the KubeClarity backend, use an application ID as defined by the KubeClarity backend.
You can find the application ID on the **Applications** screen of the UI, or you can use the KubeClarity API.

### Export SBOM

To export the SBOM to the KubeClarity backend, set the `BACKEND_HOST` environment variable and the `-e` flag.

> Note: Until TLS is supported, set `BACKEND_DISABLE_TLS=true`.

```shell
BACKEND_HOST=<KubeClarity backend address> BACKEND_DISABLE_TLS=true kubeclarity-cli analyze <image> --application-id <application ID> -e -o <SBOM output file>
```

For example:

```shell
BACKEND_HOST=localhost:9999 BACKEND_DISABLE_TLS=true kubeclarity-cli analyze nginx:latest --application-id 23452f9c-6e31-5845-bf53-6566b81a2906 -e -o nginx.sbom
```

### Export vulnerability scan results

To export the vulnerability scan results to the KubeClarity backend, set the `BACKEND_HOST` environment variable and the `-e` flag.

> Note: Until TLS is supported, set `BACKEND_DISABLE_TLS=true`.

```shell
BACKEND_HOST=<KubeClarity backend address> BACKEND_DISABLE_TLS=true kubeclarity-cli scan <image> --application-id <application ID> -e
```

For example:

```shell
SCANNERS_LIST="grype" BACKEND_HOST=localhost:9999 BACKEND_DISABLE_TLS=true kubeclarity-cli scan nginx.sbom --input-type sbom  --application-id 23452f9c-6e31-5845-bf53-6566b81a2906 -e
```
