---
title: Deploy on Kubernetes
weight: 110
---

## Prerequisites

* Install a tool to run local Kubernetes clusters. Here, [Kind](https://kind.sigs.k8s.io/) is used as the default option for creating a local cluster.
* [Helm](https://helm.sh/) to install OpenClarity.

## Deployment steps

To deploy OpenClarity to your Kubernetes cluster, complete the following steps.

1. Create a Kubernetes cluster.

    ```shell
    kind create cluster --name openclarity-k8s
    ```

1. Ensure the Kubernetes cluster is up and running. If you're using kind, you can check the status of your clusters with the following command:

    ```shell
    kind get clusters
    ````

1. Use Helm to install OpenClarity. Run the following command:

    ```shell
    helm install openclarity oci://ghcr.io/openclarity/charts/openclarity --version {{< param "latest_version" >}} \
        --namespace openclarity --create-namespace \
        --set orchestrator.provider=kubernetes \
        --set orchestrator.serviceAccount.automountServiceAccountToken=true
    ```

1. Verify that all the OpenClarity pods have been successfully deployed by executing the following command:

    ```shell
    kubectl get pods -n openclarity
    ```

1. Wait until all pods are in the `Running` state or have completed their initialization.

1. Once the pods are ready, start port forwarding to access the OpenClarity gateway service. Use the following command to forward traffic from your local machine to the cluster:

    ```shell
    kubectl port-forward -n openclarity service/openclarity-gateway 8080:80
    ````

1. Access the OpenClarity UI by navigating to [http://localhost:8080/](http://localhost:8080/) in your web browser.

    <p align="center" width="100%">
        <img width="75%" src="/img/opnclarity-ui-1.png">
    </p>

## Next steps

Complete the {{% xref "/docs/getting-started/first-tasks/_index.md" %}}.

## Clean up steps

1. Uninstall OpenClarity with Helm. Run the following command:

    ```shell
    helm uninstall openclarity --namespace openclarity
    ```

1. Delete the Kubernetes cluster.

    ```shell
    kind delete clusters openclarity-k8s
    ```