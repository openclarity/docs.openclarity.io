---
title: SBOM Output Format
weight: 800
---

The `openclarity-cli scan` command can format the resulting SBOM into different formats to integrate with another system. The supported formats are:

| Format | Configuration Name |
| --- | --- |
| CycloneDX JSON (default) | cyclonedx-json |
| CycloneDX XML | cyclonedx-xml |
| SPDX JSON | spdx-json |
| SPDX Tag Value | spdx-tv |
| Syft JSON | syft-json |

{{< warning >}}
OpenClarity processes CycloneDX internally, the other formats are supported through a conversion. The conversion process can be lossy due to incompatibilities between formats, therefore in some cases not all fields/information are present in the resulting output.
{{< /warning >}}

To configure the `openclarity-cli` to use a format other than the default, the `sbom.output_format` config parameter can be used with the configuration name from above:

```shell
ANALYZER_OUTPUT_FORMAT="spdx-json" openclarity-cli analyze nginx:latest -o nginx.sbom
```
