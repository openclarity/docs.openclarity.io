---
title: VMClarity development
weight: 2000
---

## Building VMClarity Binaries

Makefile targets are provided to compile and build the VMClarity binaries.
`make build` can be used to build all of the components, but also specific
targets are provided, for example `make build-cli` and `make build-backend` to
build the specific components in isolation.

## Building VMClarity Containers

`make docker` can be used to build the VMClarity containers for all of the
components. Specific targets for example `make docker-cli` and `make
docker-backend` are also provided.

`make push-docker` is also provided as a shortcut for building and then
publishing the VMClarity containers to a registry. You can override the
destination registry like:

```
DOCKER_REGISTRY=docker.io/tehsmash make push-docker
```

You must be logged into the docker registry locally before using this target.

## Linting

`make lint` can be used to run the required linting rules over the code.
golangci-lint rules and config can be viewed in the `.golangcilint` file in the
root of the repo.

`make fix` is also provided which will resolve lint issues which are
automatically fixable for example format issues.

`make license` can be used to validate that all the files in the repo have the
correctly formatted license header.

To lint the cloudformation template, `cfn-lint` can be used, see
https://github.com/aws-cloudformation/cfn-lint#install for instructions on how
to install it for your system.

## Unit tests

`make test` can be used run all the unit tests in the repo. Alternatively you
can use the standard go test CLI to run a specific package or test like:

```
go test ./cli/cmd/... -run Test_isSupportedFS
```

## Generating API code

After making changes to the API schema in `api/openapi.yaml`, you can run `make
api` to regenerate the model, client and server code.

## Testing End to End

For details on how to test VMClarity end to end please see {{% xref "/docs/archive/vmclarity/development/test_e2e.md" %}}.
