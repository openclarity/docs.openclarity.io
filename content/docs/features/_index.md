---
title: Features
weight: 20
---

OpenClarity provides a wide range of features for asset scanning and discovery:

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
  - Export results to OpenClarity backend
- API
  - See the {{% xref "/docs/api/_index.md" %}}.


## Runtime environment

The following table lists all supported environments and asset types that can be discovered and scanned by OpenClarity.

| Environment | Asset Type                                                         | Scope                             | 
|-------------|--------------------------------------------------------------------|-----------------------------------|
| Docker      | Containers, Container Images                                       | Docker Daemon                     |
| Kubernetes  | Containers, Container Images                                       | Cluster                           | 
| AWS         | Virtual machines                                                   | All VMs accessible by credentials | 
| Azure       | Virtual machines                                                   | All VMs accessible by credentials | 
| GCP         | Virtual machines                                                   | All VMs accessible by credentials | 
| Local (OS)  | Containers, Container Images, Container Image Archives, Filesystem | All assets accessible by OS       | 

## Scanning 

The following table lists all supported scanners that can be used when performing a scan on an asset, such as a container image or a directory.

|                                                           | VMClarity | KubeClarity | OpenClarity |
|-----------------------------------------------------------|-----------|-------------|-------------|
| **SBOM generation and analysis**                          | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Syft                             | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Trivy                            | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; cyclonedx-gomod                  | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Windows Registry                 | ✅         | ❌           | ✅         |
| **Vulnerability detection**                               | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Grype                            | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Trivy                            | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Dependency Track                 | ❌         | ✅           | ❌         |
| **Exploits**                                              | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; ExploitDB                        | ✅         | ❌           | ✅         |
| **Secrets**                                               | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Gitleaks                         | ✅         | ❌           | ✅         |
| **Malware**                                               | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; ClamAV                           | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Yara                             | ✅         | ❌           | ✅         |
| **Misconfiguration**                                      | ✅         | ✅           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Lynis                            | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; CIS Docker Benchmark             | ✅         | ✅           | ✅         |
| **Rootkits**                                              | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; Chrootkit                        | ✅         | ❌           | ✅         |
| **Plugins**                                               | ✅         | ❌           | ✅         |
| &nbsp;&nbsp;&nbsp;&nbsp; KICS                             | ✅         | ❌           | ✅         | 


## Integrated SBOM Generators and Vulnerability Scanners

{{< include-headless "kubeclarity/supported-sbom-generators.md" >}}

{{< include-headless "kubeclarity/supported-vulnerability-scanners.md" >}}
