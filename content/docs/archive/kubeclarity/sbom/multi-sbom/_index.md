---
title: Merging SBOM results
weight: 300
---

Different SBOM generators support different outputs, and the different vulnerability analyzers support different input SBOM formats. KubeClarity merges the output of multiple SBOM scanners and converts them into the format required by vulnerability scanners.

![Multi-SBOM Integration Process](merging-sbom-output.png)

When multiple analyzers identify the same resources, KubeClarity handles them as a union and labels both analyzers as the source. Instead of attempting to merge the raw data produced by each generator, KubeClarity adds additional metadata to the generated SBOMs while keeping the raw data untouched, as reported by the analyzers.

KubeClarity can also merge SBOMs from various stages of a CI/CD pipeline into a single SBOM by layering and merging, for example, application dependency SBOM analysis from application build time can be augmented with the image dependencies analysis during the image build phase. The merged SBOMs serve as inputs to vulnerability scanners after proper formatting.

![SBOM Integrations at Various CI/CD Stages](sbom-cicd-layering.png)
