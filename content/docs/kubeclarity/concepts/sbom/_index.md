---
title: Software bill of materials
linktitle: SBOM
weight: 100
---

A software bill of materials (SBOM) is a list of all the components, libraries, and other dependencies that make up a software application, along with information about the versions, licenses, and vulnerabilities associated with each component. They are formal, structured documents detailing the components of a software product and its supply chain relationships.

SBOMs are important because organizations increasingly rely on open-source and third-party software components to build and maintain their applications. These components can introduce security vulnerabilities and must be adequately managed and updated. SBOMs help you understand what open-source and third-party components are used in your applications, and identify and address any security vulnerabilities.

Under specific scenarios, generating and publishing SBOMs is mandatory for compliance with regulations and industry standards that require organizations to disclose the use of open-source and third-party software in their products.

## SBOM standards

There are several related standards, for example, CycloneDX, SPDX, SWID.

[SPDX (Software Package Data Exchange)](https://spdx.dev/) is a standard format for communicating a software package’s components, licenses, and copyrights. It is commonly used to document the open-source components included in a proprietary software product. SPDX files can be easily read and understood by humans and machines, making it easy to track and manage open-source components in a software project. SPDX format is supported by Linux Foundation.

CycloneDX is an open-source standard for creating software bill of materials files. It is like SPDX in that it documents the components and licenses associated with a software package, but it is specifically designed for use in software supply chain security. CycloneDX is a more lightweight format compared to SPDX, which is intended to be more detailed. CycloneDX format is supported by OWASP.

## SBOM architecture

A typical SBOM architecture can be laid out as a tree-like dependency graph with the following key elements:

- Component inventory: Information about the components, libraries, and other assets used in the software, including version numbers, licenses, and vulnerabilities.
- Dependency mapping: A map of relationships between different components and libraries, showing how they depend on each other and how changes to one may impact the other.
- License management: It should also include information about the licenses of the components and libraries used to ensure that the software complies with legal and ethical obligations.

## SBOM generators

There are two typical ways to generate SBOM: during the build process, or after the build and deployment using a Software Composition Analysis tool. Trivy and Syft are two noteworthy open-source generators among many other generators, including open-source and commercial. Both use CycloneDX format. It is also important to note that not all SBOMs can be generated equally. Each generator may pick up a few language libraries better than the others based on its implementation. It might take multiple runs through a few different types of generators to draw comprehensive insights.

{{< include-headless "kubeclarity/supported-sbom-generators.md" >}}

## Multiple SBOMs for accuracy

KubeClarity can run multiple SBOM generators in parallel, and unify their results to generate a more accurate document.

In such cases, KubeClarity compiles a merged SBOM from multiple open-source analyzers, and delivers a comprehensive SBOM document report. Although KubeClarity does not generate SBOMs, it integrates with popular generators so that a combined document can provide amplified inputs that can be further analyzed using vulnerability scanners. Leveraging multiple SBOM documents can improve visibility into software dependency posture.

KubeClarity formats the merged SBOM to comply with the input requirements of vulnerability scanners before starting vulnerability scans.

> Note: KubeClarity can merge vulnerability scans from various sources like Grype and Trivy to generate a robust vulnerability scan report.

## Scan SBOM documents for vulnerabilities

You can feed the generated SBOM documents to vulnerability scanners, which analyze the SBOMs and generate a vulnerability report detailing all known and fixed CVEs of the software components listed by SBOM.