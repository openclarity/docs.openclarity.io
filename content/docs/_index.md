---
title: OpenClarity Documentation
weight: 1
aliases:
- /docs/overview/
---


OpenClarity is an open source tool for agentless detection and management of Virtual Machine
Software Bill Of Materials (SBOM) and security threats such as vulnerabilities, exploits, malware, rootkits, misconfigurations and leaked secrets.


Join [OpenClarity's Slack channel](https://outshift.slack.com/messages/vmclarity) to hear about the latest announcements and upcoming activities. We would love to get your feedback!

## Table of Contents<!-- omit in toc -->

- [Why OpenClarity?](#why-Openclarity)
- [Getting started](#getting-started)
- [Overview](#overview)
  - [Asset discovery](#asset-discovery)
  - [Supported filesystems](#supported-filesystems)
- [Architecture](#architecture)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Code of Conduct](#code-of-conduct)
- [License](#license)

## Why OpenClarity?

Virtual machines (VMs) are the most used service across all hyperscalers. AWS,
Azure, GCP, and others have virtual computing services that are used not only
as standalone VM services but also as the most popular method for hosting
containers (for example, Docker, Kubernetes).

VMs are vulnerable to multiple threats:
- Software vulnerabilities
- Leaked Secrets/Passwords
- Malware
- System Misconfiguration
- Rootkits

There are many very good open source and commercial-based solutions for
providing threat detection for VMs, manifesting the different threat categories above.

However, there are challenges with assembling and managing these tools yourself:
- Complex installation, configuration, and reporting.
- Integration with deployment automation.
- Siloed reporting and visualization.

The OpenClarity project is focused on unifying detection and management of VM security threats in an agentless manner.

## Getting Started

For step-by-step guidance on how to deploy OpenClarity across different environments, including AWS, Azure, GCP, and Docker, see [Getting Started](docs/getting-started/_index.md) and choose your preferred provider for detailed deployment instructions.

## Overview

OpenClarity uses a pluggable scanning infrastructure to provide:
- SBOM analysis
- Package and OS vulnerability detection
- Exploit detection
- Leaked secret detection
- Malware detection
- Misconfiguration detection
- Rootkit detection

The pluggable scanning infrastructure uses several tools that can be
enabled/disabled on an individual basis. OpenClarity normalizes, merges and
provides a robust visualization of the results from these various tools.

These tools include:

- SBOM Generation and Analysis
  - [Syft](https://github.com/anchore/syft)
  - [Trivy](https://github.com/aquasecurity/trivy)
  - Windows Registry*
  - [Cyclonedx-gomod](https://github.com/CycloneDX/cyclonedx-gomod)
- Vulnerability detection
  - [Grype](https://github.com/anchore/grype)
  - [Trivy](https://github.com/aquasecurity/trivy)
- Exploits
  - [Go exploit db](https://github.com/vulsio/go-exploitdb)
- Secrets
  - [gitleaks](https://github.com/gitleaks/gitleaks)
- Malware
  - [ClamAV](https://github.com/Cisco-Talos/clamav)
  - [YARA](https://github.com/virustotal/yara)
- Misconfiguration
  - [Lynis](https://github.com/CISOfy/lynis)**
  - [CIS Docker Benchmark](https://github.com/goodwithtech/dockle)
  - [KICS](https://github.com/Checkmarx/kics)
- Rootkits
  - [Chkrootkit](https://github.com/Magentron/chkrootkit)**


\* Windows only\
** Linux and MacOS only

### Asset Discovery

The OpenClarity stack supports the automatic discovery of assets in the following providers:

| Provider   | Asset types                      | Scope                 | Installation                                                     |
|------------|----------------------------------|-----------------------|------------------------------------------------------------------|
| Docker     | Docker containers and images     | Local Docker daemon   | {{% xref "/docs/getting-started/deploy-docker/_index.md" %}} |
| Kubernetes | Docker containers and images     | Cluster               | {{% xref "/docs/getting-started/deploy-kubernetes/_index.md" %}}  |
| AWS        | Virtual machines (EC2 instances) | Account (all regions) | {{% xref "/docs/getting-started/deploy-aws/_index.md" %}}  |
| Azure      | Virtual machines                 | Subscription          | {{% xref "/docs/getting-started/deploy-azure/_index.md" %}}  |
| GCP        | Virtual machines                 | Project               | {{% xref "/docs/getting-started/deploy-gcp/_index.md" %}}  |


## Supported Filesystems

The following filesystem operations are supported on different host types:

| Host    | List block devices | Mount Ext2, Ext3, Ext4 | Mount XFS     | Mount NTFS    |
|---------|--------------------|------------------------|---------------|---------------|
| Linux   | Supported          | Supported              | Supported     | Supported     |
| Darwin  | Supported          | Supported              | Supported     | Supported     |
| Windows | Not supported      | Not supported          | Not supported | Not supported |

## Architecture
A high-level architecture overview is available under [OpenClarity Stack]({{% relref "/docs/usage/openclarity_stack.md" %}}).

## Roadmap
The OpenClarity project roadmap is available [here](https://github.com/orgs/openclarity/projects/5/views/5).

## Contributing

If you are ready to jump in and test, add code, or help with documentation,
please follow the instructions on our [contributing guide](CONTRIBUTING.md)
for details on how to open issues and setup OpenClarity for development and testing.

## Code of Conduct

You can view our code of conduct [here](CODE_OF_CONDUCT.md).

## License

[Apache License, Version 2.0](LICENSE.md)