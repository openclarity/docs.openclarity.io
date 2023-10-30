---
title: "Kubernetes Security"
weight: 1000
github_project_repo: "https://github.com/openclarity/kubeclarity/"
cascade:
  github_project_repo: "https://github.com/openclarity/kubeclarity/"
---

Kubernetes Security is a tool for detection and management of Software Bill Of Materials (SBOM) and vulnerabilities of container images and filesystems. It scans both runtime K8s clusters and CI/CD pipelines for enhanced software supply chain security.

![Kubernetes Security dashboard screenshot](dashboard.png)

## Why?
### SBOM & Vulnerability Detection Challenges

- Effective vulnerability scanning requires an accurate Software Bill Of Materials (SBOM) detection:
  - Various programming languages and package managers
  - Various OS distributions
  - Package dependency information is usually stripped upon build
- Which one is the best scanner/SBOM analyzer?
- What should we scan: Git repos, builds, container images or runtime?
- Each scanner/analyzer has its own format - how to compare the results?
- How to manage the discovered SBOM and vulnerabilities?
- How are my applications affected by a newly discovered vulnerability?

### Solution

- Separate vulnerability scanning into 2 phases:
  - Content analysis to generate SBOM
  - Scan the SBOM for vulnerabilities
- Create a pluggable infrastructure to:
  - Run several content analyzers in parallel
  - Run several vulnerability scanners in parallel
- Scan and merge results between different CI stages using Kubernetes Security CLI
- Runtime K8s scan to detect vulnerabilities discovered post-deployment
- Group scanned resources (images/directories) under defined applications to navigate the object tree dependencies (applications, resources, packages, vulnerabilities)

## Architecture

![Kubernetes Security architecture diagram](architecture.png)

## Limitations

1. Supports Docker Image Manifest V2, Schema 2 (https://docs.docker.com/registry/spec/manifest-v2-2/). It will fail to scan earlier versions.

## Roadmap
- Integration with additional content analyzers (SBOM generators)
- Integration with additional vulnerability scanners
- CIS Docker benchmark in UI
- Image signing using [Cosign](https://github.com/sigstore/cosign)
- CI/CD metadata signing and attestation using [Cosign](https://github.com/sigstore/cosign) and [in-toto](https://github.com/in-toto/in-toto) (supply chain security)
- System settings and user management
