# argocd-local-k8s-app-set

Helm charts repository for automated Argo CD applications provisioning in the local k8s cluster.

## Argo CD Setup

### Clean up all minikube data:

- `minikube stop`
- `minikube delete --all=true --purge=true`

### Set configurations and start minikube:

- `minikube config set cpus 12`
- `minikube config set memory 16384`
- `minikube config view`
- `minikube start`

### Install Argo CD and connect to Web UI:

- `helm repo add argoproj-community https://argoproj.github.io/argo-helm`
- `helm dep update ./charts/argo-cd-wrapper/`
- `helm install argo-cd ./charts/argo-cd-wrapper/ --namespace="argo-cd" --create-namespace`
- `kubectl port-forward svc/argo-cd-argocd-server 8099:443 --namespace="argo-cd"`

### Install Applications provisioner manifests:

- `helm template ./charts/argo-cd-applications-provisioner/ | kubectl apply -f -`

## Bitnami PostgreSQL

### Install PostgreSQL

- `helm dep update ./charts/bitnami-postgresql-wrapper/`
