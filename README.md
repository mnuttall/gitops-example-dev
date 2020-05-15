# gitops-example-dev

This repository illustrates the repository file format supported by the tool being developed in https://github.com/rhd-gitops-example/services. It represents the deployment configuration for one or more microservices (also known as 'components') for a 'dev' environment. Microservices are aggregated into [applications](https://github.com/kubernetes-sigs/application) under the 'apps' directory.

See our companion repository https://github.com/rhd-gitops-example/gitops-example-staging which represents a second environment from which services are 'promoted' to, from this 'dev' environment.

Environment-specific configuration is held in the /overlays directories, and may be applied at the level of a single service, an application, or the entire environment.

To see things working:

```sh
kustomize build environments/dev/services/service-a
kustomize build environments/dev/apps/app-1
kustomize build environments
```

or `kubectl apply -k` these paths

## `namespace` considerations

The Kubernetes namespace that a repository in this format would be deployed in would typically be defined in a `namespace.yaml` file in `env/base/`.

The recommended best practice for deploying an individual app or service into a different namespace would be to:

1. Create the namespace.

`kubectl create namespace my_namespace`

2. Clone the GitOps repo.

`git clone https://github.com/rhd-gitops-example/gitops-example-dev`

3. Apply the app or service you want to your namespace.

```
kustomize build services/service-a | kubectl apply -n my_namespace -f -
kustomize build apps/app-a | kubectl apply -n my_namespace -f -
```
