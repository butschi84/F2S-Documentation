---
sidebar_position: 1
---

# Deployment

F2S can be deployed on your kubernetes cluster by using the official HELM chart.

Add the HELM Repository
```
helm repo add f2s https://butschi84.github.io/F2S/helm-release
helm repo update
```

Install F2S CRDs. F2S Uses a Kubernetes Custom Ressource Definition (CRDs) "functions.f2s.opensight.ch" to configure functions.
```
# install crds
kubectl apply -f https://butschi84.github.io/F2S/helm-release/crds/crds.yaml
```

## Deploy F2S
Next step is to deploy the HELM Chart.
```
helm install f2s f2s/f2s
```

## HELM Chart Values

### Test Functions
F2S - per default - will be deployed with some example functions (CRD Function Definitions). That can be disabled by modifying the testfunctions.enabled value in the HELM Chart
```
# deploy 2 testfunction CRDs
testfunctions:
  enabled: true
```

### Promtail Configuration
Per default, F2S will not deploy Promtail Containers. If you are running your own Instance of Grafana Loki, you can deploy Promtail by enabling this parameter in the HELM chart. That will deploy a promtail daemonset an collect the logs of the "f2s operator" container(s).

```
# enable promtail to gather logs
# you need your own loki instance
promtail:
  enabled: false
  loki_url: http://loki-loki-distributed-gateway.loki:80/loki/api/v1/push
```

### Grafana
F2S HELM Chart can deploy a grafana instance, preconfigured with some useful dashboards, that provide insight to current F2S Traffic and Scaling. The deployment of the grafana instance can be disabled by modifying this configuration settings.
```
# deploy grafana to have insight into metrics
# - f2s scaling decision dashboard
# - f2s traffic dashboard
grafana:
  enabled: true

```