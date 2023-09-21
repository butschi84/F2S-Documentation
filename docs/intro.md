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
  * TODO Security (OAuth)
* **Authorization**<br/>
  Authorization (RBAC)
* **Kafka**<br/>
  TODO Kafka Message Bus Integration

## Core Concept

* Keep it as simple as can be
* Run out of the box with as few dependencies as possible. <br/>
  No service meshes or other dependencies
* Simple start. Up and running in default config in 1 minute
* Lightweight. Use the features of vanilla kubernetes where ever possible
* Intuitive. No steep learning curve<br/>
  Beginners can use a UI to manage the soultion (i.e. create the CRD’s using the UI)
* No "enterprise only" features