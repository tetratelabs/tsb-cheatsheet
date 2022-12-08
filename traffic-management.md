---
title: Traffic Management
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: Traffic Management
intro: 
  Traffic management in TSB.
---

## Intro

### Resources

- [`IngressGateway`](#ingressgateway) Workload to act as a gateway for traffic entering the mesh (north-south)

## IngressGateway

### Sample

#### sample/traffic-management/ingressgateway.yaml
```yaml
apiVersion: gateway.tsb.tetrate.io/v2
kind: IngressGateway
metadata:
  name: bookinfo-ingress
  group: bookinfo-gatewaygroup
  workspace: bookinfo-workspace
  tenant: bookinfo
  organization: tsbdemo
spec:
  workloadSelector:
    namespace: bookinfo
    labels:
      app: bookinfo-gateway
  http:
  - name: bookinfo-plaintext
    port: 80
    hostname: bookinfo.com
    routing:
      rules:
      - redirect:
          authority: bookinfo.com
          port: 443
          redirectCode: 301
          scheme: https
  - name: bookinfo-secure
    port: 443
    hostname: bookinfo.com
    tls:
      mode: SIMPLE
      secretName: bookinfo-cert
    routing:
      rules:
      - route:
          host: ns1/productpage.ns1.svc.cluster.local
          port: 9080
```

### Fields

Interpretations of fields in the sample
- `workloadSelector`: gateway with `app: bookinfo-gateway` label will be the edge proxy.
- `http`: application type.
- `routing`: rules for traffic flows.
- `tls`: tls mode and location of certs if required.
