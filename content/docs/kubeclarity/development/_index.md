---
title: VMClarity development
weight: 2000
---

## Building KubeClarity

`make build` will build all of the KubeClarity code and UI.

Makefile targets are provided to compile and build the KubeClarity binaries.
`make build-all-go` can be used to build all of the go components, but also
specific targets are provided, for example `make cli` and `make backend` to
build the specific components in isolation.

`make ui` is provided to just build the UI components.

## Building KubeClarity Containers

`make docker` can be used to build the KubeClarity containers for all of the
components. Specific targets for example `make docker-cli` and `make
docker-backend` are also provided.

`make push-docker` is also provided as a shortcut for building and then
publishing the KubeClarity containers to a registry. You can override the
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
automaticlly fixable for example format issues.

`make license` can be used to validate that all the files in the repo have the
correctly formatted license header.

## Unit tests

`make test` can be used run all the unit tests in the repo. Alternatively you
can use the standard go test CLI to run a specific package or test by going
into a specific modules directory and running:

```
cd cli
go test ./cmd/... -run <test name regex>
```

## Generating API code

After making changes to the API schema for example `api/swagger.yaml`, you can run `make
api` to regenerate the model, client and server code.

## Testing End to End

End to end tests will start and exercise a KubeClarity running on the local
container runtime. This can be used locally or in CI. These tests ensure that
more complex flows such as the CLI exporting results to the API work as
expected.

> ***Note***:
> If running Docker Desktop for Mac you will need to increase docker daemon
> memory to 8G. Careful, this will drain a lot from your computer cpu.

In order to run end-to-end tests locally:

```shell
# Build all docker images
make docker
# Replace Values In The KubeClarity Chart:
sed -i 's/latest/${{ github.sha }}/g' charts/kubeclarity/values.yaml
sed -i 's/Always/IfNotPresent/g' charts/kubeclarity/values.yaml
# Build the KubeClarity CLI
make cli
# Move the Built CLI into the E2E Test folder
mv ./cli/bin/cli ./e2e/kubeclarity-cli
# Run the end to end tests
make e2e
```

## Sending Pull Requests

Before sending a new pull request, take a look at existing pull requests and issues to see if the proposed change or fix
has been discussed in the past, or if the change was already implemented but not yet released.

We expect new pull requests to include tests for any affected behavior, and, as we follow semantic versioning, we may
reserve breaking changes until the next major version release.
