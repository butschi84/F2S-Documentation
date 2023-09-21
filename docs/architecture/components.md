---
sidebar_position: 1
---

# F2S Architecture

F2S consists of the following components, both of which are deployed in the Kubernetes "f2s" namespace.

* **F2S Operator**
* **Prometheus**

## F2S Operator

The F2S Operator consists of a single binary, that is executed in a container. F2S Operator runs in the "F2S" namespace and is configured to use 2 replicas. The F2S Operators have no shared state other then the Metrics that are stored in the Prometheus Instance. Those Metrics are used to make container scaling decisions and also to determine which F2S Operator should be "master".

The binary itself encompasses the following internal components:

![](/img/architecture.png)

* **API Server**<br/>
  'API Server' is the REST API Interface. Functions can be defined and invoked via API. Authentication and Authorization are part of 'API Server'. All function invocations are then sent to 'dispatcher'.
* **Metrics**<br/>
  F2S Exposes Metrics in order to be able to make scaling decisions and have insight in all activity
* **Config**<br/>
  The Config package observes CRD's (F2SFunction Declarations) in "f2s" namespace on kubernetes
* **Kafka**<br/>
  Package for Interaction with Kafka Event Bus (planned). All invocations are sent to dispatcher.
* **Operator**<br/>
  Operator reacts to Config Changes and creates or deletes deployments and services in f2s-containers namespace. It is also responsible for scaling functions up and down.
* **Dispatcher**<br/>
  Dispatcher picks up all incoming requests (REST, Kafka) and decides which function pod should serve the request.

# Prometheus
The Prometheus instance collects the metrics from the running F2S Operator(s), as well as some Kube State Metrics. The metrics are used by the operator to make scaling decisions.