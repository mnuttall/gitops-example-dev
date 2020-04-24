# gitops-example-dev

This repository illustrates the repository file format supported by the tool being developed in https://github.com/rhd-gitops-example/services. It represents the deployment configuration for one or more microservices (also known as 'components') for a 'dev' environment. Microservices are aggregated into [applications](https://github.com/kubernetes-sigs/application) under the 'apps' directory.

See our companion repository https://github.com/rhd-gitops-example/gitops-example-staging which represents a second environment from which services are 'promoted' to, from this 'dev' environment.

Environment-specific configuration is held in the /overlays directories, and may be applied at the level of a single service, an application, or the entire environment.

To see things working:

```sh
kustomize build services/service-a
kustomize build apps/app-1
kustomize build env
```

or `kubectl apply -k` these paths
