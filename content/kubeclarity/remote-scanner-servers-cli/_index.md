---
title: Remote scanner servers for CLI
linktitle: Remote scanner servers
weight: 1500
---

When running the KubeClarity CLI to scan for vulnerabilities, the CLI needs to download the relevant vulnerability databases to the location where the KubeClarity CLI is running. Running the CLI in a CI/CD pipeline will result in downloading the databases on each run, wasting time and bandwidth. For this reason, several of the supported scanners have a remote mode in which a server is responsible for the database management and possibly scanning of the artifacts.

> Note: The examples below are for each of the scanners, but they can be combined to run together the same as they can be in non-remote mode.
