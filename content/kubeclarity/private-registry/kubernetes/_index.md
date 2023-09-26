---
title: Private registry support for Kubernetes
linktitle: Kubernetes
weight: 200
---

KubeClarity uses [k8schain](https://github.com/google/go-containerregistry/tree/main/pkg/authn/k8schain#k8schain) for authenticating to the registries. If the necessary service credentials are not discoverable by the k8schain, you can define them as secrets as described below.

In addition, if service credentials are not located in the `kubeclarity` namespace, set `CREDS_SECRET_NAMESPACE` to `kubeclarity` Deployment.

When using Helm [charts](https://github.com/openclarity/kubeclarity/tree/main/charts/kubeclarity), `CREDS_SECRET_NAMESPACE` is set to the release namespace installed kubeclarity.

## Amazon ECR

1. Create an [AWS IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console) with `AmazonEC2ContainerRegistryFullAccess` permissions.

1. Use the user credentials (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_DEFAULT_REGION`) to create the following secret:

    ```yaml
    cat <<EOF | kubectl apply -f -
    apiVersion: v1
    kind: Secret
    metadata:
      name: ecr-sa
      namespace: kubeclarity
    type: Opaque
    data:
      AWS_ACCESS_KEY_ID: $(echo -n 'XXXX'| base64 -w0)
      AWS_SECRET_ACCESS_KEY: $(echo -n 'XXXX'| base64 -w0)
      AWS_DEFAULT_REGION: $(echo -n 'XXXX'| base64 -w0)
    EOF
    ```

    > Note:
    > - The name of the secret must be `ecr-sa`
    > - The secret data keys must be set to `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_DEFAULT_REGION`

## Google GCR

1. Create a [Google service account](https://cloud.google.com/docs/authentication/getting-started#creating_a_service_account) with `Artifact Registry Reader` permissions.

1. Use the service account json file to create the following secret:

    ```shell
    kubectl -n kubeclarity create secret generic --from-file=sa.json gcr-sa
    ```

    > Note:
    > - Secret name must be `gcr-sa`
    > - `sa.json` must be the name of the service account json file when generating the secret
    > - KubeClarity is using [application default credentials](https://developers.google.com/identity/protocols/application-default-credentials). These only work when running KubeClarity from GCP.
