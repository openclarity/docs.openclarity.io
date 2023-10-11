---
title: Set configuration file location for the CLI
linktitle: CLI configuration file location
weight: 1200
---

The default configuration path of the CLI is `$HOME/.kubeclarity`. To specify a different file, use the `--config` flag, like this:

```shell
kubeclarity-cli <scan/analyze> <image name> --config <kubeclarity config path>
```

For example:

```shell
kubeclarity-cli scan registry/nginx:private --config $HOME/own-kubeclarity-config
```
