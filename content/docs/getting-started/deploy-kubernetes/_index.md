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
    kind create cluster --name vmclarity-k8s
    ```

1. Ensure the Kubernetes cluster is up and running. If you're using kind, you can check the status of your clusters with the following command:

    ```shell
    kind get clusters
    ````

1. Use Helm to install OpenClarity. Run the following command:

    ```shell
    helm install vmclarity oci://ghcr.io/openclarity/charts/vmclarity --version {{< param "latest_version" >}} \
        --namespace vmclarity --create-namespace \
        --set orchestrator.provider=kubernetes \
        --set orchestrator.serviceAccount.automountServiceAccountToken=true
    ```

1. Verify that all the OpenClarity pods have been successfully deployed by executing the following command:

    ```shell
    kubectl get pods -n vmclarity
    ```

1. Wait until all pods are in the `Running` state or have completed their initialization.

1. Once the pods are ready, start port forwarding to access the OpenClarity gateway service. Use the following command to forward traffic from your local machine to the cluster:

    ```shell
    kubectl port-forward -n vmclarity service/vmclarity-gateway 8080:80
    ````

1. Access the OpenClarity UI by navigating to [http://localhost:8080/](http://localhost:8080/) in your web browser.

    <p align="center" width="100%">
        <img width="75%" src="/img/vmclarity-ui-1.png">
    </p>

## Next steps

Complete the {{% xref "/docs/getting-started/first-tasks/_index.md" %}}.

## Clean up steps

1. Uninstall OpenClarity with Helm. Run the following command:

    ```shell
    helm uninstall vmclarity --namespace vmclarity
    ```

1. Delete the Kubernetes cluster.

    ```shell
    kind delete clusters vmclarity-k8s
    ```