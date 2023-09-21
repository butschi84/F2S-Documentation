---
sidebar_position: 2
---

# Configuration
F2S is configured by a configmap "f2s-conf" in the "f2s" kubernetes namespace, which contains the data of "config.yaml". This chapter describes the possible configuration options. 

## Debug Mode
Logging can be configured for a higher verbosity by enabling the debug mode:
```
# enable debug output
+ debug: true
```

## Prometheus URL
Prometheus is a critical component for F2S. By modifying the prometheus.url parameter in the configmap, you can point f2s to another prometheus instance.
This parameter can also be modified by setting the environment variable 'Prometheus_URL'. In most cases, you should not modify this configuration property, because it points per default to the prometheus instance which is deployed by the f2s helm chart.
```
prometheus:
  url: prometheus-service.f2s:9090
```

## Timeouts
Timeouts can be configured in the configmap. F2S will abort those requests that exceed a timeout period.

* scaling_timeout<br />
  When zero replicas of a function are available, f2s will scale up the deployment from zero to one.
* http_timeout<br />
  How long should f2s wait at maximum for completion of a backend function
* request timeout<br />
  timeout for completion of the whole request


![](/img/timeouts.png)

## Authentication
Right now, F2S Supports the Authentication Modes:

**none**<br />
Just allow all requests. Authorization Controls are also disabled in Authentication Mode 'none'.

```
f2s:
  auth:
    global_config:
      type: none
```

**basic**<br />
HTTP basic auth.

```
f2s:
  auth:
    global_config:
      type: basic
    basic:
      - username: roman
        password: helloworld
        group: admins
```

**token**<br />
Authentication with a jwt bearer token.

```
f2s:
  auth:
    global_config:
      type: token
    token:
      tokens:
        - token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MjQyMzc4OTgsImdyb3VwIjoiZ3JvdXAxIiwic3ViIjoicm9tYW4ifQ.xQOtzG2cNa4eg97qidR-YN7v3qyJ18qjShWYLFUs_bU
      jwt_secret: test
```

## Authorization
Each user Account can be assigned to a group. Global Privileges are then assigned to the group via F2S Configmap

```
f2s:
  ...
  auth:
    ...
    authorization:
      - group: admins
        privileges:
          - functions:list
          - functions:invoke
          - functions:create
          - functions:delete
          - functions:update
          - settings:view
          - settings:update

```

## Example Configuration
Here is some complete example configuration

```
# enable debug output
# debug: true

prometheus:
  url: prometheus-service.f2s:9090

f2s:
  timeouts:
    request_timeout: 120000
    http_timeout: 60000
    scaling_timeout: 45000
   auth:
    global_config:
      type: token
#   basic:
#     - username: roman
#       password: helloworld
#       group: group1
    token:
      tokens:
        - token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MjQyMzc4OTgsImdyb3VwIjoiZ3JvdXAxIiwic3ViIjoicm9tYW4ifQ.xQOtzG2cNa4eg97qidR-YN7v3qyJ18qjShWYLFUs_bU
      jwt_secret: test
```