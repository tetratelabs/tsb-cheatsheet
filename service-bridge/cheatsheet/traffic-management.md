---
title: Traffic Settings Management
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: Resources
intro: 
  <a href='https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/traffic/v2/yaml'>Traffic Settings Management</a> in TSB.
---

## Intro

### Resources

- TrafficGroup allow grouping the proxy workloads in a set of namespaces owned by its parent workspace
- [`ServiceRoute`](#serviceroute) Define versions of services with traffic shifting policies
- [`TrafficSetting`](#trafficsetting) Define behavior of proxy workloads

### tsb/traffic/v2
- [`TrafficGroup`](https://docs.tetrate.io/service-bridge/1.5.x/en-us/refs/tsb/traffic/v2/traffic_group)
- [`ServiceRoute`](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/traffic/v2/service_route)
- [`TrafficSetting`](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/traffic/v2/traffic_setting)


## ServiceRoute

### Sample

#### sample/traffic-management/serviceroute.yaml

```yaml
apiVersion: traffic.tsb.tetrate.io/v2
kind: ServiceRoute
Metadata:
  organization: tsbdemo
  tenant: bookinfo
  workspace: bookinfo-workspace
  group: bookinfo-trafficgroup
  name: bookinfo-tg-reviews
spec:
  service: bookinfo/reviews.bookinfo.svc.cluster.local
  stickySession:
    useSourceIp: true
  subsets:
    - name: v1
      labels:
        version: v1
      weight: 50
    - name: v2
      labels:
        version: v2
      weight: 50
```
### Fields

Interpretations of fields in the sample
- `service`: which service configuration will be applied
- `stickySession`: how to keep traffic from client to a specific backend
- `subsets`: a list of versions with traffic weights

## TrafficSetting

### Sample

#### sample/traffic-management/trafficsetting.yaml

```yaml
apiVersion: traffic.tsb.tetrate.io/v2
kind: TrafficSetting
metadata:
  organization: tsbdemo
  tenant: bookinfo
  workspace: bookinfo-workspace
  group: bookinfo-trafficgroup
  name: bookinfo-tg
spec:
  resilience:
    httpRetries:
      attempts: 3
      perTryTimeout: 3s
      retryOn: 5xx,gateway-error,reset
```

### Fields

Interpretations of fields in the sample
- `resillience`: traffic reliability knobs 
- `httpRetries`: retry policy for all HTTP requests