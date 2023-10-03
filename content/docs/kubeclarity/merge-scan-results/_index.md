---
title: Merge scan results
weight: 1200
---

You can merge SBOM and vulnerabilities scan results into a single file. For example, you can merge the scan results across different CI/CD stages.

To merge an existing SBOM into the final results, use the `--merge-sbom <existing-sbom-file>` flag during analysis. The input SBOM can be in CycloneDX XML or CyclonDX JSON format. (For details on output formats, see {{% xref "/docs/kubeclarity/output-sbom-format/_index.md" %}}).

For example:

```shell
ANALYZER_LIST="syft" kubeclarity-cli analyze nginx:latest -o nginx.sbom --merge-sbom inputsbom.xml
```
