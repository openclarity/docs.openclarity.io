---
title: SBOM output format
weight: 800
---

The `kubeclarity-cli analyze` command can format the resulting SBOM into different formats to integrate with another system. The supported formats are:

| Format | Configuration Name |
| --- | --- |
| CycloneDX JSON (default) | cyclonedx-json |
| CycloneDX XML | cyclonedx-xml |
| SPDX JSON | spdx-json |
| SPDX Tag Value | spdx-tv |
| Syft JSON | syft-json |

{{< warning >}}
Kubernetes Security processes CycloneDX internally, the other formats are supported through a conversion. The conversion process can be lossy due to incompatibilities between formats, therefore in some cases not all fields/information are present in the resulting output.
{{< /warning >}}

To configure the `kubeclarity-cli` to use a format other than the default, the `ANALYZER_OUTPUT_FORMAT` environment variable can be used with the configuration name from above:

```shell
ANALYZER_OUTPUT_FORMAT="spdx-json" kubeclarity-cli analyze nginx:latest -o nginx.sbom
```
