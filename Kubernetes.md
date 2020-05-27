# Kubernetes

You can also deploy Foundry VTT on your K8S/K3S cluster using different approachs.

## Kustomize 
by [mbround18](https://github.com/mbround18/)

Requirements:

* Kubernetes Cluster (EKS/GKE/AKS/K3S/K8S)

Follow the detailed step on the his [repo](https://github.com/mbround18/foundryvtt-docker/blob/master/README.md#installation-on-kubernetes).


## Helm Charts
by [Hugo Prudente](https://github.com/hugoprudente/)

Requirements:

* Helm 
* Kubernetes Cluster (EKS/GKE/AKS/K3S/K8S)
* Container built with [Felddy's Easy Container](https://github.com/felddy/foundryvtt-docker.git)

```shell
git clone https://github.com/hugoprudente/charts/
```

Edit the file `values.yaml` with your desired configuration.

```shell
helm install --name foundry ./incubator/foundry-vtt
```

