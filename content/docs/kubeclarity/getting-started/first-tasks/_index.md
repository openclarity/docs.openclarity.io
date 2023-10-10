---
title: First tasks - CLI
weight: 300
---

After you have [installed the KubeClarity backend]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-backend/_index.md" >}}) and the [KubeClarity CLI]({{< relref "/docs/kubeclarity/getting-started/install-kubeclarity-cli/_index.md" >}}), complete the following tasks to see the basic functionality of KubeClarity, either using the CLI, or using the [web UI]({{< relref "/docs/kubeclarity/getting-started/first-tasks-ui/_index.md" >}}).

## Generate SBOM

{{< include-headless "kubeclarity/generate-sbom-simple-cli.md" >}}

## Vulnerability scan

You can scan vulnerabilities by running the appropriate commands. The CLI provides flexibility and automation capabilities for integrating vulnerability scanning into your existing workflows or CI/CD pipelines. The tool allows scanning an image, directory, file, or a previously generated SBOM.

Usage:

```shell
kubeclarity-cli scan <image/sbom/directory/file name> --input-type <sbom|dir|file|image(default)> -f <output file>
```

Example:

```shell
kubeclarity-cli scan nginx.sbom --input-type sbom
```

You can list the vulnerability scanners to use using the `SCANNERS_LIST` environment variable separated by a space (`SCANNERS_LIST="<Scanner1 name> <Scanner2 name>"`). For example:

```shell
SCANNERS_LIST="grype trivy" kubeclarity-cli scan nginx.sbom --input-type sbom
```

Example output:

```shell
INFO[0000] Called trivy scanner on source sbom nginx.sbom  app=kubeclarity scanner=trivy
INFO[0000] Loading DB. update=true                       app=kubeclarity mode=local scanner=grype
INFO[0000] Need to update DB                             app=kubeclarity scanner=trivy
INFO[0000] DB Repository: ghcr.io/aquasecurity/trivy-db  app=kubeclarity scanner=trivy
INFO[0000] Downloading DB...                             app=kubeclarity scanner=trivy
INFO[0010] Gathering packages for source sbom:nginx.sbom  app=kubeclarity mode=local scanner=grype
INFO[0010] Found 136 vulnerabilities                     app=kubeclarity mode=local scanner=grype
INFO[0011] Sending successful results                    app=kubeclarity mode=local scanner=grype
INFO[0011] Got result for job "grype"                    app=kubeclarity
INFO[0012] Vulnerability scanning is enabled             app=kubeclarity scanner=trivy
INFO[0012] Detected SBOM format: cyclonedx-json          app=kubeclarity scanner=trivy
INFO[0012] Detected OS: debian                           app=kubeclarity scanner=trivy
INFO[0012] Detecting Debian vulnerabilities...           app=kubeclarity scanner=trivy
INFO[0012] Number of language-specific files: 1          app=kubeclarity scanner=trivy
INFO[0012] Detecting jar vulnerabilities...              app=kubeclarity scanner=trivy
INFO[0012] Sending successful results                    app=kubeclarity scanner=trivy
INFO[0012] Found 136 vulnerabilities                     app=kubeclarity scanner=trivy
INFO[0012] Got result for job "trivy"                    app=kubeclarity
INFO[0012] Merging result from "grype"                   app=kubeclarity
INFO[0012] Merging result from "trivy"                   app=kubeclarity
NAME              INSTALLED                FIXED-IN  VULNERABILITY     SEVERITY    SCANNERS
curl              7.74.0-1.3+deb11u7                 CVE-2023-23914    CRITICAL    grype(*), trivy(*)
curl              7.74.0-1.3+deb11u7                 CVE-2023-27536    CRITICAL    grype(*), trivy(*)
libcurl4          7.74.0-1.3+deb11u7                 CVE-2023-27536    CRITICAL    grype(*), trivy(*)
libdb5.3          5.3.28+dfsg1-0.8                   CVE-2019-8457     CRITICAL    grype(*), trivy(*)
libcurl4          7.74.0-1.3+deb11u7                 CVE-2023-23914    CRITICAL    grype(*), trivy(*)
perl-base         5.32.1-4+deb11u2                   CVE-2023-31484    HIGH        grype(*), trivy(*)
libss2            1.46.2-2                           CVE-2022-1304     HIGH        grype(*), trivy(*)
bash              5.1-2+deb11u1                      CVE-2022-3715     HIGH        grype(*), trivy(*)
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
