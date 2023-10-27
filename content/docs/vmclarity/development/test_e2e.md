---
title: End-to-End Testing Guide
weight: 480
---

## Installing a specific VMClarity build on AWS

1. Build the containers and publish them to your docker registry

    ```ini
    DOCKER_REGISTRY=<your docker registry> make push-docker
    ```

1. Install VMClarity cloudformation

    1. Ensure you have an SSH key pair uploaded to AWS Ec2
    2. Go to **CloudFormation -> Create Stack -> Upload** template.
    3. Upload the `VMClarity.cfn` file.
    4. Follow the wizard through to the end
        1. Set the `VMClarity Backend Container Image` and `VMClarity Scanner Container Image` parameters in the wizard to use custom images (from step 1.) for deployment.
        1. Change the Asset Scan Delete Policy to `OnSuccess` or `Never` if debugging scanner VMs is required.
    5. Wait for install to complete

1. Ensure that VMClarity backend is working correctly

    1. Get the IP address from the CloudFormation stack's Output Tab
    2. `ssh ubuntu@<ip address>`
    3. Check the VMClarity Logs

        ```shell
        sudo journalctl -u vmclarity
        ```

## Performing an end to end test

1. Copy the example [scanConfig.json](scanConfig.json) into the ubuntu user's home directory

    ```shell
    scp scanConfig.json ubuntu@<ip address>:~/scanConfig.json
    ```

2. Edit the scanConfig.json

    1. Give the scan config a unique name
    1. Enable the different scan families you want:

        ```yaml
        "scanFamiliesConfig": {
          "sbom": {
            "enabled": true
          },
          "vulnerabilities": {
            "enabled": true
          },
          "exploits": {
            "enabled": true
          }
        },
        ```

    1. Configure the scope of the test

        - By Region, VPC or Security group:

            ```yaml
            "scope": "contains(assetInfo.location, '<name of region>/<name of vpc>') and contains(assetInfo.securityGroups, '{\"id\":\"<name of sec group>\"}')"
            ```

        - By tag:

            ```yaml
            "scope": "contains(assetInfo.tags, '{\"key\":\"<key>\",\"value\":\"<value>\"}')"
            ```

      - All:

            ```yaml
            "scope": ""
            ```

    1. Set operationTime to the time you want the scan to run. As long as the time is in the future it can be within seconds.

3. While ssh'd into the VMClarity server run

    ```shell
    curl -X POST http://localhost:8080/api/scanConfigs -H 'Content-Type: application/json' -d @scanConfig.json
    ```

4. Check VMClarity logs to ensure that everything is performing as expected

    ```shell
    sudo journalctl -u vmclarity
    ```

5. Monitor the asset scans

    - Get scans:

        ```shell
        curl -X GET http://localhost:8080/api/scans
        ```

        After the operationTime in the scan config created above there should be a new
        scan object created in Pending.

        Once discovery has been performed, the scan's assetIDs list should be
        populated will all the assets to be scanned by this scan.

        The scan will then create all the "assetScans" for tracking the scan
        process for each asset. When that is completed the scan will move to
        "InProgress".

    -  Get asset scans:

        ```shell
        curl -X GET http://localhost:8080/api/assetScans
        ```
