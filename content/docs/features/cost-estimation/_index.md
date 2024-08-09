---
title: Cost Estimation
wight: 400
---

Available in version 0.6.0 and later. Currently, this feature is exclusively available on AWS.

You can get a preliminary cost estimation before initiating a security scan with OpenClarity. This helps you plan and budget your security assessments more effectively, ensuring that you have a clear understanding of the financial implications before taking action.

To start a new estimation, complete the following steps.

1. Create a new resource called `ScanEstimation` in the API server. For example, if your POST's body is the following JSON, it will estimate an SBOM scan on your workload with id `i-123456789`.

    Use the same same `scanTemplate` in the  `ScanEstimation` than in the `ScanConfiguration`.

    ```yaml
    {
      "assetIDs": ["i-123456789"],
      "state": {
        "state": "Pending"
      },
      "scanTemplate": {
        "scope": "contains(assetInfo.tags, '{\"key\":\"scanestimation\",\"value\":\"test\"}')",
        "assetScanTemplate": {
          "scanFamiliesConfig": {
            "sbom": {
              "enabled": true
            }
          }
        }
      }
    }
    ```

1. Retrieve the object from the `<apiserver IP address>:8888/scanEstimations` endpoint, and wait for the state to be `Done`. The `totalScanCost` of the summary property shows your scan's cost in USD:

    ```yaml
    {
       "assetIDs":[
          "d337bd07-b67f-4cf0-ac43-f147fce7d1b2"
       ],
       "assetScanEstimations":[
          {
             "id":"23082244-0fb6-4aca-8a9b-02417dfc95f8"
          }
       ],
       "deleteAfter":"2023-10-08T17:33:52.512829081Z",
       "endTime":"2023-10-08T15:33:52.512829081Z",
       "id":"962e3a10-05fb-4c5d-a773-1198231f3103",
       "revision":5,
       "scanTemplate":{
          "assetScanTemplate":{
             "scanFamiliesConfig":{
                "sbom":{
                   "enabled":true
                }
             }
          },
          "scope":"contains(assetInfo.tags, '{\"key\":\"scanestimation\",\"value\":\"test\"}')"
       },
       "startTime":"2023-10-08T15:33:37.513073573Z",
       "state":{
          "state":"Done",
          "stateMessage":"1 succeeded, 0 failed out of 1 total asset scan estimations",
          "stateReason":"Success"
       },
       "summary":{
          "jobsCompleted":1,
          "jobsLeftToRun":0,
          "totalScanCost":0.0006148403,
          "totalScanSize":3,
          "totalScanTime":12
       },
       "ttlSecondsAfterFinished":7200
    }
    ```
