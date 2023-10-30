---
title: Features
weight: 200
---


- Dashboard
  - Fixable vulnerabilities per severity
  - Top 5 vulnerable elements (applications, resources, packages)
  - New vulnerabilities trends
  - Package count per license type
  - Package count per programming language
  - General counters
- Applications
  - Automatic application detection in K8s runtime
  - Create/edit/delete applications
  - Per application, navigation to related:
    - Resources (images/directories)
    - Packages
    - Vulnerabilities
    - Licenses in use by the resources
- Application Resources (images/directories)
  - Per resource, navigation to related:
    - Applications
    - Packages
    - Vulnerabilities
- Packages
    - Per package, navigation to related:
        - Applications
        - Linkable list of resources and the detecting SBOM analyzers
        - Vulnerabilities
- Vulnerabilities
    - Per vulnerability, navigation to related:
        - Applications
        - Resources
        - List of detecting scanners
- K8s Runtime scan
  - On-demand or scheduled scanning
  - Automatic detection of target namespaces
  - Scan progress and result navigation per affected element (applications, resources, packages, vulnerabilities)
  - CIS Docker benchmark
- CLI (CI/CD)
  - SBOM generation using multiple integrated content analyzers (Syft, cyclonedx-gomod)
  - SBOM/image/directory vulnerability scanning using multiple integrated scanners (Grype, Dependency-track)
  - Merging of SBOM and vulnerabilities across different CI/CD stages
  - Export results to Kubernetes Security backend
- API
  - See {{% xref "/docs/kubeclarity/api/_index.md" %}}.

## Integrated SBOM generators and vulnerability scanners

{{< include-headless "kubeclarity/supported-sbom-generators.md" >}}

{{< include-headless "kubeclarity/supported-vulnerability-scanners.md" >}}
