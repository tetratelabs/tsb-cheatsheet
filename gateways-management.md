---
title: Gateways Management
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: Gateways
intro:
  Gateways Management
---

## Intro

### Resources

- [`Install IngressGateway`](#install-ingressgateway) Define method to install IngressGateway on k8s/ocp
- [`Configure IngressGateway`](#configure-ingressgateway) Defines destination host for traffic entering the mesh and traffic routing policies (north-south)
- [`Install Tier1Gateway`](#install-tier1gateway) Define method to install Tier1Gateway on k8s/ocp
- [`Configure Tier1Gateway`](#configure-ingressgateway) Defines way to configure workload to act as a gateway that distributes traffic across one or more ingress gateways


## Install IngressGateway

### Sample

#### sample/traffic-management/installingressgateway.yaml

```yaml
apiVersion: install.tetrate.io/v1alpha1
kind: IngressGateway
metadata:
  name: bookinfo-ingressgateway
  namespace: bookinfo
spec:
  kubeSpec:
    service:
      type: LoadBalancer
```

### Details

- using `kubectl` or `oc` to create IngressGateway deployment

## Configure IngressGateway

### Sample

#### sample/traffic-management/ingressgateway.yaml
```yaml
apiVersion: gateway.tsb.tetrate.io/v2
kind: IngressGateway
metadata:
  organization: tsbdemo
  tenant: bookinfo
  workspace: bookinfo-workspace
  group: bookinfo-gatewaygroup
  name: bookinfo-ingress
spec:
  workloadSelector:
    namespace: bookinfo
    labels:
      app: bookinfo-gateway
  http:
  - name: bookinfo-plaintext
    port: 80
    hostname: bookinfo.tetrate.com
    routing:
      rules:
      - redirect:
          authority: bookinfo.tetrate.com
          port: 443
          redirectCode: 301
          scheme: https
  - name: bookinfo-secure
    port: 443
    hostname: bookinfo.tetrate.com
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

## Install Tier1Gateway

### Sample

#### sample/traffic-management/installtier1gateway.yaml

```yaml
apiVersion: install.tetrate.io/v1alpha1
kind: Tier1Gateway
metadata:
  name: bookinfo-tier1-gateway
  namespace: tier1
spec:
  kubeSpec:
    service:
      type: LoadBalancer
```

### Details

- using `kubectl` or `oc` to create Tier1Gateway deployment

## Configure Tier1Gateway

### Sample

#### sample/traffic-management/ingressgateway.yaml

```yaml
---
apiVersion: gateway.tsb.tetrate.io/v2
kind: Tier1Gateway
metadata:
  organization: tsbdemo
  tenant: bookinfo
  workspace: bookinfo-workspace
  group: bookinfo-tier1-gg
  name: bookinfo-tier1
spec:
  workloadSelector:
    namespace: tier1
    labels:
      app: bookinfo-tier1-gateway
  externalServers:
  - hostname: bookinfo.tetrate.com
    name: bookinfo
    port: 443
    tls:
      mode: SIMPLE
      secretName: bookinfo-certs
    clusters:
    - name: c1
      weight: 90
    - name: c2
      weight: 10
```

### Fields

Interpretations of fields in the sample
- `workloadSelector`: gateway with `app: bookinfo-gateway` label will be the edge proxy.
- `externalServers`: servers exposed by the gateway externally.
- `tls`: tls mode and location of certs if required.
- `clusters`: The destination clusters that contain ingress gateways exposing the hostname.