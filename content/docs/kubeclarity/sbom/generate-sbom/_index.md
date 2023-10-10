---
title: Generate SBOM
weight: 100
---

{{< include-headless "kubeclarity/generate-sbom-simple-cli.md" >}}

## Export scan results to backend

1. {{< include-headless "kubeclarity/get-application-id.md" >}}
1. {{< include-headless "kubeclarity/export-sbom-scan-results.md" >}}
1. Now you can see the exported results on the UI. For the `nginx` image, the **SBOM Analyzers** column now also displays `trivy`.

    ![Exported results](multi-sbom-export-ui.png)

## Run multiple generators

You can list the content analyzers to use using the `ANALYZER_LIST` environment variable separated by a space (`ANALYZER_LIST="<analyzer 1 name> <analyzer 2 name>"`). For example:

```shell
ANALYZER_LIST="syft gomod" kubeclarity-cli analyze --input-type image nginx:latest -o nginx.sbom
```

{{< include-headless "kubeclarity/supported-sbom-generators.md" >}}
