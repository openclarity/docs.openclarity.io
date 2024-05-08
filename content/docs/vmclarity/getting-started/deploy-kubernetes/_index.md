---
title: Deploy on Kubernetes
weight: 110
---

## Prerequisites

* Install a tool to run local Kubernetes clusters. Here, [Kind](https://kind.sigs.k8s.io/) is used as the default option for creating a local cluster.
* Install a package manager. Here, [Helm](https://helm.sh/) is used as the default installer.

## Deployment steps

To deploy VMClarity to your Kubernetes cluster, complete the following steps.

1. Ensure the Kubernetes cluster is up and running. If you're using kind, you can check the status of your clusters with the following command:

    ```shell
    kind get clusters
    ````

1. Use Helm to install VMClarity. Run the following command, making sure to replace installation/kubernetes/helm/vmclarity with the correct path to the VMClarity Helm chart:

    ```shell
    helm install vmclarity installation/kubernetes/helm/vmclarity \
        --namespace vmclarity --create-namespace \
        --set orchestrator.provider=kubernetes \
        --set orchestrator.serviceAccount.automountServiceAccountToken=true \
        --set exploitDBServer.containerSecurityContext.enabled=false
    ```

1. Verify that all the VMClarity pods have been successfully deployed by executing the following command:

    ```shell
    kubectl get pods -n vmclarity
    ```

1. Wait until all pods are in the `Running` state or have completed their initialization.

1. Once the pods are ready, start port forwarding to access the VMClarity gateway service. Use the following command to forward traffic from your local machine to the cluster:

    ```shell
    kubectl port-forward -n vmclarity service/vmclarity-gateway 8080:80
    ````

1. Access the VMClarity UI by navigating to [http://localhost:8080/](http://localhost:8080/) in your web browser.

    <p align="center" width="100%">
        <img width="75%" src="/img/vmclarity-ui-1.png">
    </p>

## Next steps

Complete the {{% xref "/docs/vmclarity/getting-started/first-tasks/_index.md" %}}.
