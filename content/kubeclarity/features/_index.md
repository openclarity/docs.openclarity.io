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
  - Export results to KubeClarity backend
- API
  - The API for KubeClarity can be found [here](https://github.com/openclarity/kubeclarity/blob/master/api/swagger.yaml)

## Integrated SBOM generators and vulnerability scanners

KubeClarity content analyzer integrates with the following SBOM generators:

- [Syft](https://github.com/anchore/syft)
- [Cyclonedx-gomod](https://github.com/CycloneDX/cyclonedx-gomod)
- [Trivy](https://github.com/aquasecurity/trivy)

KubeClarity vulnerability scanner integrates with the following scanners:

- [Grype](https://github.com/anchore/grype)
- [Dependency-Track](https://github.com/DependencyTrack/dependency-track)
- [Trivy](https://github.com/aquasecurity/trivy)
