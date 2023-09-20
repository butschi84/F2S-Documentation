---
sidebar_position: 1
---

# Overview

F2S is an open source **Functions as a Service** Platform, that can run on a Kubernetes Cluster.

## Getting Started

Get started by by **installing on your kubernetes**.
This will install f2s on your kubernetes cluster.

* "Functions" CRD
* Namespaces "f2s", "f2s-containers"
* ClusterRoles and Bindings
* Deployments for F2S, Grafana, Prometheus
* Services

```
helm repo add f2s https://butschi84.github.io/F2S/helm-release
helm repo update

# install crds
kubectl apply -f https://butschi84.github.io/F2S/helm-release/crds/crds.yaml

# install f2s
helm install f2s f2s/f2s
```

# Features
These are the main feeatures of F2S

* **Gitops**<br/>
  Define your Functions as K8S CRDs
* **Scale to Zero**<br/>
  Can scale Deployments to zero when there is no activity
* **Autoscaling**<br/>
  F2S continuously measures the performance of your containers and uses the data for autoscaling
* **Authentication**<br/>
  Right now, F2S Supports Token (JWT) Authentication and Basic Auth
  * None
  * Token (JWT)
  * Basic Auth
  * <font color=orange>TO DO</font> Security (OAuth)
* **Authorization**<br/>
  Authorization (RBAC)
* **Kafka**<br/>
  <font color=orange>TO DO</font> Kafka Message Bus Integration