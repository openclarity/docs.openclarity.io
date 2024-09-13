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
# Create config based on https://github.com/openclarity/openclarity/blob/main/.families.yaml
cat <<EOF > config.yml
sbom:
  enabled: true
  analyzers_list:
    - "syft"
  inputs:
    - input: "/dir-to-scan"
      input_type: "rootfs"
  output_format: "cyclonedx-json"
EOF

# Run scan
openclarity-cli scan --config config.yml
```

For more information the CLI configuration, see the [Example CLI Configuration]({{< relref "/docs/usage/command_line/cli_reference.md" >}}).