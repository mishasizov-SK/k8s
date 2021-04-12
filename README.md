# TrustBloc Deployment

The repo contains the scripts to deploy the core TrustBloc components.

## Prerequisites
- docker (running)
- [minikube](#minikube)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)  [minimum version: v1.20]
- GNU bash [minimum version: v5] (for macOS, refer [macos setup](#macos-additional-prerequisites))
- GNU make
- GNU sed

### Minikube 
Currently, the [deployment fails](https://github.com/trustbloc/k8s/issues/9) with minikube v1.19. Follow the 
instructions to install v1.18 for TrustBloc k8s deployment.

```
# macOS amd64
curl -LO https://github.com/kubernetes/minikube/releases/download/v1.18.0/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube

# linux
curl -LO https://github.com/kubernetes/minikube/releases/download/v1.18.0/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### MacOS additional prerequisites
- [HyperKit](https://minikube.sigs.k8s.io/docs/drivers/hyperkit/) installed
- Install GNU sed and base64 utils: `brew install gnu-sed coreutils bash`
- Create directory with symlinks to the used GNU tools
  ```
  # mkdir ~/gnu && cd ~/gnu && ln -fs $( which gsed ) sed && ln -fs $( which gbase64 ) base64
  ```
- Always prepend the directory with GNU tools to the PATH when using this repo or add this to the bash profile, e.g.:
  ```
  # PATH=~/gnu:$PATH
  ```

## Running

Re-create any existing minikube cluster and deploy all trustbloc services into the newly created cluster:

`make setup-and-deploy`

Deploy all components to the existing kubernetes cluster:

`make`

Deploy specific components to the existing kubernetes cluster:

`make deploy-components COMPONENTS="component1 component2 component3"`

Minikube cluster setup:

`make minikube-setup`

Minikube cluster re-create:

`make minikube-reset`

## Kubernetes Dashboard

To access the dashboard run `kubectl port-forward svc/kubernetes-dashboard -n kubernetes-dashboard 8888:80` and browse to the port-forwarded URL: http://localhost:8888

## Contributing
Thank you for your interest in contributing. Please see our [community contribution guidelines](https://github.com/trustbloc/community/blob/main/CONTRIBUTING.md) for more information.

## License
Apache License, Version 2.0 (Apache-2.0). See the [LICENSE](LICENSE) file.
