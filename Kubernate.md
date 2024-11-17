# Kubernete Cluster on Docker
-------

### Prerequisite
* ([Docker](https://www.docker.com/products/docker-desktop/)
* Install kind (https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

Save the below in cluster.yaml file

``` bash
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
  extraPortMappings:
  - containerPort: 80
    hostPort: 80
    protocol: TCP
  - containerPort: 443
    hostPort: 443
    protocol: TCP
- role: control-plane
- role: control-plane
- role: worker
- role: worker
- role: worker

```

## Run the following command
``` bash
kind create cluster --config cluster.yaml --name my-cluster

```
