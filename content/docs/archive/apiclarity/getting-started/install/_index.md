---
title: Install APIClarity
weight: 100
---

<!-- FIXME Prerequisites (Istio) -->

## Install APIClarity in a K8s cluster using Helm

1. Add the Helm repository.

   ```shell
   helm repo add apiclarity https://openclarity.github.io/apiclarity
   ```

1. Save the default chart values into the `values.yaml` file.

    ```shell
    helm show values apiclarity/apiclarity > values.yaml
    ```

    > Note: The file [values.yaml](https://github.com/openclarity/apiclarity/blob/master/charts/apiclarity/values.yaml) is used to deploy and configure APIClarity on your cluster via Helm. [This ConfigMap](https://github.com/openclarity/apiclarity/blob/master/charts/apiclarity/templates/configmap.yaml) is used to define the list of headers to ignore when reconstructing the spec.

1. Update `values.yaml` with the required traffic source values.
1. Deploy APIClarity with Helm.

   ```shell
   helm install --values values.yaml --create-namespace apiclarity apiclarity/apiclarity --namespace apiclarity
   ```

1. Port forward to the APIClarity UI:

   ```shell
   kubectl port-forward --namespace apiclarity svc/apiclarity-apiclarity 9999:8080
   ```

1. Open the APIClarity UI in your browser at `http://localhost:9999/`
1. Generate some traffic in the traced applications, for example, [using a demo application]({{< relref "/docs/archive/apiclarity/getting-started/install-demo-application/_index.md" >}}).
1. Check the APIClarity UI.

### Uninstall APIClarity from Kubernetes using Helm

1. Uninstall the Helm deployment.

   ```shell
   helm uninstall apiclarity --namespace apiclarity
   ```

1. Clean the resources. By default, Helm will not remove the PVCs and PVs for the StatefulSets. Run the following command to delete them all:

    ```shell
    kubectl delete pvc -l app.kubernetes.io/instance=apiclarity --namespace apiclarity
    ```

## Build from source

1. Build and push the image to your repo:

    ```shell
    DOCKER_IMAGE=<your docker registry>/apiclarity DOCKER_TAG=<your tag> make push-docker
    ```

1. Update [values.yaml](https://github.com/openclarity/apiclarity/blob/master/charts/apiclarity/values.yaml) accordingly.

## Run locally with demo data

1. Build the UI and the backend locally.

   ```shell
   make ui && make backend
   ```

1. Copy the built site:

   ```shell
   cp -r ./ui/build ./site
   ```

1. Run the backend and frontend locally using demo data:

   Note: You might need to delete the old local state file and local db:

   ```shell
   rm state.gob; rm db.db
   ```

   ```shell
   DATABASE_DRIVER=LOCAL K8S_LOCAL=true FAKE_TRACES=true FAKE_TRACES_PATH=./backend/pkg/test/trace_files \
   ENABLE_DB_INFO_LOGS=true ./backend/bin/backend run
   ```

   > Note: this command requires a proper KUBECONFIG in your environment when __K8S_LOCAL=true__ is used. If you want to run without Kubernetes, use __ENABLE_K8S=false__ instead.

1. Open the APIClarity UI in your browser at: `http://localhost:8080/`
