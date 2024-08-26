---
title: Common CLI tasks
linktitle: OpenClarity CLI
weight: 410
---

## Initiate a Scan Using the CLI

## Reporting Results into File:
```
./cli/bin/vmclarity-cli scan --config ~/testConf.yaml -o outputfile
```

If we want to report results to the OpenClarity backend, we need to create asset and asset scan object before scan because it requires asset-scan-id

## Reporting Results to OpenClarity Backend:

```
ASSET_ID=$(./cli/bin/vmclarity-cli asset-create --file assets/dir-asset.json --server http://localhost:8080/api) --jsonpath {.id}
ASSET_SCAN_ID=$(./cli/bin/vmclarity-cli asset-scan-create --asset-id $ASSET_ID --server http://localhost:8080/api) --jsonpath {.id}
./cli/bin/vmclarity-cli scan --config ~/testConf.yaml --server http://localhost:8080/api --asset-scan-id $ASSET_SCAN_ID
```

Using one-liner:
```
./cli/bin/vmclarity-cli asset-create --file docs/assets/dir-asset.json --server http://localhost:8080/api --update-if-exists --jsonpath {.id} | xargs -I{} ./cli/bin/vmclarity-cli asset-scan-create --asset-id {} --server http://localhost:8080/api --jsonpath {.id} | xargs -I{} ./cli/bin/vmclarity-cli scan --config ~/testConf.yaml --server http://localhost:8080/api --asset-scan-id {}
```