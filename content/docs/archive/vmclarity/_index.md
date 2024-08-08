---
title: VM Security
weight: 5
aliases:
- /docs/overview/
github_project_repo: "https://github.com/openclarity/vmclarity/"
cascade:
  github_project_repo: "https://github.com/openclarity/vmclarity/"
---

VMClarity is an open source tool for agentless detection and management of Virtual Machine Software Bill Of Materials (SBOM) and security threats such as vulnerabilities, exploits, malware, rootkits, misconfigurations and leaked secrets.

VMClarity is the tool responsible for VM Security in the OpenClarity platform.

<img src="/img/vmclarity_demo.gif" alt="VMClarity demo" />

Join [VMClarity's Slack channel](https://outshift.slack.com/messages/vmclarity) to hear about the latest announcements and upcoming activities. We would love to get your feedback!

## Why VMClarity?

Virtual machines (VMs) are the most used service across all hyperscalers. AWS,
Azure, GCP, and others have virtual computing services that are used not only
as standalone VM services but also as the most popular method for hosting
containers (e.g., Docker, Kubernetes).

VMs are vulnerable to multiple threats:
- Software vulnerabilities
- Leaked Secrets/Passwords
- Malware
- System Misconfiguration
- Rootkits

There are many very good open source and commercial-based solutions for
providing threat detection for VMs, manifesting the different threat categories above.

However, there are challenges with assembling and managing these tools yourself:
- Complex installation, configuration, and reporting
- Integration with deployment automation
- Siloed reporting and visualization

The VMClarity project is focused on unifying detection and management of VM security threats in an agentless manner.

## Overview

VMClarity uses a pluggable scanning infrastructure to provide:
- SBOM analysis
- Package and OS vulnerability detection
- Exploit detection
- Leaked secret detection
- Malware detection
- Misconfiguration detection
- Rootkit detection

The pluggable scanning infrastructure uses several tools that can be
enabled/disabled on an individual basis. VMClarity normalizes, merges and
provides a robust visualization of the results from these various tools.

These tools include:
- SBOM Generation and Analysis
  - [Syft](https://github.com/anchore/syft)
  - [Trivy](https://github.com/aquasecurity/trivy)
  - [Cyclonedx-gomod](https://github.com/CycloneDX/cyclonedx-gomod)
- Vulnerability detection
  - [Grype](https://github.com/anchore/grype)
  - [Trivy](https://github.com/aquasecurity/trivy)
  - [Dependency-Track](https://github.com/DependencyTrack/dependency-track)
- Exploits
  - [Go exploit db](https://github.com/vulsio/go-exploitdb)
- Secrets
  - [gitleaks](https://github.com/gitleaks/gitleaks)
- Malware
  - [ClamAV](https://github.com/Cisco-Talos/clamav)
  - [YARA](https://virustotal.github.io/yara/)) (Available in version 0.6.0 and later)
- Misconfiguration
  - [Lynis](https://github.com/CISOfy/lynis)
- Rootkits
  - [Chkrootkit](https://github.com/Magentron/chkrootkit)

A high-level architecture overview is available in {{% xref "/docs/vmclarity/architecture/architecture.md" %}}.

## Roadmap

VMClarity project roadmap is available [here](https://github.com/orgs/openclarity/projects/2/views/7).
