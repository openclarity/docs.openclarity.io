---
title: Announcing VMClarity v0.6.0
publishDate: 2023-11-16
tags: [vmclarity, openclarity]
---

VMClarity, Cisco's production ready **workload scanning software** has just rolled out its latest release, v0.6.0. In this blog post, we'll explore the standout features of this release that promise to enhance your experience with it.

VMClarity is designed to empower organizations with comprehensive workload scanning and security assessment solutions, ensuring the integrity and safety of their cloud and container environments. If you’re not familiar with it, check out the [GitHub repository](https://github.com/openclarity/vmclarity), or some of the related [articles](https://techblog.cisco.com/tags/vmclarity) on our blog.

## New Features and Enhancements

### [GCP](https://cloud.google.com/) (Google Cloud Platform) Support:
VMClarity v0.6.0 introduces seamless support for GCP. Now, **you can effortlessly install VMClarity on your GCP infrastructure**, extending the platform's reach to new horizons. I'll walk you through the step-by-step process of installing VMClarity on GCP, ensuring a smooth and successful deployment.

Navigate to the `/installation/gcp/dm` folder and copy the config file before you add the required fields based on the `vmclarity.py.schema` file.

```shell
cp vmclarity-config.example.yaml vmclarity-config.yaml
```

Now that the config is copied you can edit it to add the required fields, check `vmclarity.py.schema` for optional parameters.
Let's create your deployment with the gcloud command.

```shell
gcloud deployment-manager deployments create <vmclarity deployment name> --config vmclarity-config.yaml
```

After it, just create an SSH tunnel as you would for any other environment and you can start sending HTTP request to the apiserver service.

```shell
ssh -L 8888:localhost:8888 vmclarity@<VMClarity server IP address>
```

### [Docker](https://www.docker.com/) Support:
In addition to GCP, **VMClarity now extends its compatibility to Docker environments**. Whether you're managing containers or working with microservices, VMClarity offers comprehensive scanning capabilities within Docker, ensuring your security assessments cover every corner of your infrastructure.

It was crucial for us to add Docker support, as it's a fundamental element for the end-to-end testing framework. We provided a [guide](https://github.com/openclarity/vmclarity/blob/main/installation/docker/README.md) in the repository about how to run VMClarity in Docker on your local machine so if you are curious, check it out!

To try it out locally, navigate to the `/installation/docker` folder, there is a file named `image_override.env` which enables you to try out the images you build yourself. If you issue the following command on the CLI then every control plane element will be started with a docker compose file.

```shell
docker compose --project-name vmclarity --file docker-compose.yml up -d --wait --remove-orphans
```

After Docker has set up the services, you should be able to see the running control plane containers in your Docker desktop and start sending HTTP requests to the apiserver.

![Docker desktop](https://hackmd.io/_uploads/r19eUd6ep.png)

### Cost Estimation preview:
One of the most exciting additions in this release is the Cost Estimation capability. As a user, **you can now get a preliminary cost estimation before initiating a security scan** with VMClarity. This invaluable feature helps you plan and budget your security assessments more effectively, ensuring you have a clear understanding of the financial implications before taking action.

As we work on showing this information for you on the UI, we're also gearing up to expand our offerings to other cloud providers. Currently, this feature is exclusively available on AWS.

You can start a new estimation by creating a new resource called `ScanEstimation` in the api server. For example, if your POST's body is the following JSON then it will estimate an SBOM scan on your workload with id `i-123456789`. The `ScanEstimation` has to contain the same `scanTemplate` as in the `ScanConfiguration` in order to estimate the scan properly.

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

If you are curious, you can use the endpoint `<apiserver IP address>:8888/scanEstimations` to get the object, and wait for the state to be `Done`, the `totalScanCost` of the summary property shows your scan's cost in USD:

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

## And many more!

### Arm Architecture Support for Control Plane Elements:
With VMClarity v0.6.0, we're pleased to announce that **the Docker images of the control plane elements are now available in arm64 architecture, in addition to amd64**. This expansion ensures compatibility with a broader range of hardware and deployment options.

The introduction of multi-architecture images in VMClarity holds significant importance as it enables users to run end-to-end tests locally on increasingly common arm based MacBooks.

We also updated the cloudformation file so that you can now deploy VMClarity on arm64 based AWS AMI images as well. For further information about how to install VMClarity on AWS follow the [instructions](https://github.com/openclarity/vmclarity/blob/main/installation/aws/README.md) in the repository.

### End-to-End Test Framework:
We understand the importance of rigorous testing in delivering reliable software. In this release, **we've set up an end-to-end test framework that is seamlessly integrated into our CI/CD flow**.

If you choose to contribute, please consider including end-to-end tests as part of your contributions. A small [guide](https://github.com/openclarity/vmclarity/blob/main/e2e/README.md) about how we imagine writing new tests for the new features.

### [YARA]((https://virustotal.github.io/yara/)) Malware Scanner:
Security is at the core of VMClarity's mission. In v0.6.0, **we've integrated the yara malware scanner into the platform**. This powerful addition enhances your security assessments by detecting and identifying known malware and threats, providing an extra layer of protection for your workloads.

If you want to use this new scanner then you only have to enable the malware scanner when creating a new `ScanConfig` and yara will run automatically besides the already existing [clam](https://www.clamav.net/) scanner.

## What's Coming Next

VMClarity v0.6.0 is the next step towards providing an even more comprehensive and user-friendly solution for workload scanning. A sneak peek of what's coming next:

### Kubernetes Support:
In our relentless pursuit of enhancing VMClarity's capabilities, we're actively working on [Kubernetes](https://kubernetes.io) support. Soon, you'll be able to **seamlessly integrate VMClarity with your Kubernetes clusters**, making it easier than ever to ensure the security of your containerized workloads.

### UI for Cost Estimation:
We understand that user-friendly interfaces play a crucial role in simplifying complex tasks. That's why we're developing the **user interface for the Cost Estimation** feature. This will provide a more intuitive and visual way to plan and budget your security scans, giving you greater control and clarity.

### IAM (Identity and Access Management):
Your security and access control are paramount. We're also hard at work on an IAM feature, which will **provide fine-grained control over user permissions and access rights within VMClarity**. Stay in full command of your security posture with this upcoming feature.

## Summary

If you have any questions regarding VMClarity and its usage, please do not hesitate to contact us on our [Slack](https://outshift.slack.com/) channel.

Thank you for being a part of this journey, and we look forward to the exciting developments that lie ahead!
