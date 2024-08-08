---
title: Enable external trace sources support
linktitle: External trace sources
weight: 500
---

If you enable external trace sources support, APIClarity can receive the trace sources from the entities that are external to the Kubernetes cluster. External trace sources such as Gateways and Load balancers can communicate with APIClarity to report APIs and send the traces.

## Supported Trace Sources

APIClarity can support with the following trace sources and follow the instructions per required integration.

* Apigee X Gateway
  * [Integration instructions](https://github.com/openclarity/apiclarity/tree/master/plugins/gateway/apigeex)
* BIG-IP LTM Load balancer
  * [Integration instructions](https://github.com/openclarity/apiclarity/tree/master/plugins/gateway/f5-bigip)
* Kong
  * [Integration instructions](https://github.com/openclarity/apiclarity/tree/master/plugins/gateway/kong)
* Tyk
  * [Integration instructions](https://github.com/openclarity/apiclarity/tree/master/plugins/gateway/tyk)

## Deploy APIClarity with support for external trace sources

<!-- FIXME single-source with the getting started -->

1. Add Helm Repo

    ```shell
    helm repo add apiclarity https://openclarity.github.io/apiclarity
    ```

1. Update values.yaml with:

    ```shell
    Apiclarity -> tls -> enabled as true
    supportExternalTraceSource -> enabled as true
    ```

1. Deploy APIClarity with the updated `values.yaml` to enable external traffic sources.

    ```shell
    helm install --values values.yaml --create-namespace apiclarity apiclarity/apiclarity -n apiclarity
    ```

1. Port forward to the APIClarity UI:

    ```shell
    kubectl port-forward -n apiclarity svc/apiclarity-apiclarity 9999:8080
    ```

1. Open the APIClarity UI in your browser at `http://localhost:9999`

## Register a new external trace source

This section shows you how to access the service, register a new trace source, and how to receive the token and certificate. The examples use the Apigee X Gateway as the external trace source.

1. Port forward for service at 8443.

    ```shell
    kubectl port-forward -n apiclarity svc/apiclarity-apiclarity 8443:8443
    ```

1. Register a new external trace source and receive the token.

    ```shell
    TRACE_SOURCE_TOKEN=$(curl --http1.1 --insecure -s -H 'Content-Type: application/json' -d '{"name":"apigee_gateway","type":"APIGEE_X"}' https://localhost:8443/api/control/traceSources|jq -r '.token')
    ```

1. Get the External-IP for the `apiclarity-external` service.

    ```shell
    kubectl get services --namespace apiclarity
    ```

1. Use the External-IP address with the following command, then extract the certificate between `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` and save it to the `server.crt` file.

    ```shell
    openssl s_client -showcerts -connect <External-IP>:10443
    ```

1. If you want to configure other trace sources, use the extracted token in Step 2 and the certificate in Step 3.
