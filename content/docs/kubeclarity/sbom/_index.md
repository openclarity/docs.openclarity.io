---
title: Generate SBOM
weight: 700
---

KubeClarity exposes SBOM generator integration settings via the `values.yaml` file.

{{< include-headless "kubeclarity/supported-sbom-generators.md" >}}

Trivy has an extensive vulnerability database, which includes CVEs from various sources such as NVD, Red Hat, and Debian. It can detect vulnerabilities in multiple programming languages, including Java, Python, and Ruby.

Syft’s vulnerability database is smaller and primarily focuses on detecting vulnerabilities in Python libraries.

KubeClarity, by default, enables Syft and CycloneDX gomod analyzers. To enable the Trivy scanner, edit the `values. yaml` file like this:

```yaml
    analyzer:
      ## Space separated list of analyzers. (syft gomod)
      analyzerList: "syft gomod trivy"
      analyzerScope: "squashed"

      trivy:
        ## Enable trivy scanner, if true make sure to add it to list above  
        enabled: true
        timeout: "300"
```

## SBOM database

KubeClarity automatically deploys an SBOM database pod and caches the generated SBOMs in the SBOM DB. The database is a lightweight SQLite DB that avoids persistent volume storage overheads. It stores and retrieves SBOM documents in a string format and serves as a caching function for rendering SBOM data. The DB does not store or query JSON objects to parse or query the SBOMs. However, it supports a gzip compression and base64 encoded storage to reduce memory footprint.

Here is the corresponding configuration snippet from the `values.yaml` file:

```yaml
## KubeClarity SBOM DB Values

kubeclarity-sbom-db:
  ## Docker Image values.
  docker:
    ## Use to overwrite the global docker params
    ##
    imageName: ""

  ## Logging level (debug, info, warning, error, fatal, panic).
  logLevel: warning

  servicePort: 8080

  resources:
    requests:
      memory: "20Mi"
      cpu: "10m"
    limits:
      memory: "100Mi"
      cpu: "100m"

## End of KubeClarity SBOM DB Values
```
