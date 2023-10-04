---
title: Kubernetes clusters runtime scans
weight: 200
linktitle: Runtime scans
---

Scanning your runtime Kubernetes clusters is essential to proactively detect and address vulnerabilities in real-time, ensuring the security and integrity of your applications and infrastructure. By continuously monitoring and scanning your clusters, you can mitigate risks, prevent potential attacks, and maintain a strong security posture in the dynamic Kubernetes environment.

## Runtime scan features

KubeClarity enhance the runtime scanning experience:

### Faster runtime scans

KubeClarity optimizes the scanning process, reducing the time required to detect vulnerabilities. This allows for quicker identification and remediation of potential security risks.

### Reduce image TAR pulling

KubeClarity uses an efficient approach that avoids the unnecessary overhead of fetching the complete image tar.

### Cache SBOMs

If an image has already been scanned, KubeClarity uses the cached SBOM data, avoiding time-consuming image retrieval and recomputing, improving overall efficiency.

## Runtime scan architecture

The following figure illustrates the structure of a runtime scanning architecture. This layout visually represents the components and their interconnections within the runtime scanning system.

![KubeClarity Runtime Scan Architecture](runtime-scan-architecture.png)
