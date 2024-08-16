---
title: Install demo application
weight: 200
---

If you want to use a demo application to try APIClarity, you can use the [Sock Shop Demo](https://microservices-demo.github.io/). To deploy the Sock Shop Demo, complete the following steps.

1. Create the `sock-shop` namespace and enable Istio injection.

    ```shell
    kubectl create namespace sock-shop
    kubectl label namespaces sock-shop istio-injection=enabled
    ```

1. Deploy the Sock Shop Demo to your cluster.

    ```shell
    kubectl apply -f https://raw.githubusercontent.com/microservices-demo/microservices-demo/master/deploy/kubernetes/complete-demo.yaml
    ```

1. Deploy APIClarity in the `sock-shop` namespace (with the Istio service-mesh traffic source):

    ```shell
    helm repo add apiclarity https://openclarity.github.io/apiclarity
    ```

    ```shell
    helm install --set 'trafficSource.envoyWasm.enabled=true' --set 'trafficSource.envoyWasm.namespaces={sock-shop}' --create-namespace apiclarity apiclarity/apiclarity --namespace apiclarity
    ```

1. Port forward to Sock Shop's front-end service to access the Sock Shop Demo App:

    ```shell
    kubectl port-forward -n sock-shop svc/front-end 7777:80
    ```

1. Open the Sock Shop Demo App UI in your browser at `http://localhost:7777/` and run some transactions to generate data to review on the APIClarity dashboard.
