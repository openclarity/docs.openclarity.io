---
title: Private registry support for the CLI
linktitle: CLI
weight: 100
---

The KubeClarity CLI can read a configuration file that stores credentials for private registries.

Example registry section of the configuration file:

```yaml
registry:
  auths:
    - authority: <registry 1>
      username: <username for registry 1>
      password: <password for registry 1>
    - authority: <registry 2>
      token: <token for registry 2>
```

Example registry configuration without authority: (in this case these credentials will be used for all registries):

```yaml
registry:
  auths:
    - username: <username>
      password: <password>
```
