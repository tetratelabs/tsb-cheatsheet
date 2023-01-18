---
title: kubectl CLI
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: CLI
intro: 
  Create objects with kubectl
---

## kubectl

### Quicklinks

- [TSB gitops](https://docs.tetrate.io/service-bridge/1.5.x/en-us/howto/gitops/gitops)
- [TSB CRD Reference](https://docs.tetrate.io/service-bridge/1.5.x/en-us/reference/k8s-api/guide)

## TSB Resource Management

### Sample

#### sample/tsb/workspace.yaml

```yaml
apiVersion: tsb.tetrate.io/v2
kind: Workspace
metadata:
  name: bookinfo-workspace
  annotations:
    tsb.tetrate.io/organization: tetrate
    tsb.tetrate.io/tenant: dev
spec:
  displayName: bookinfo-workspace
  namespaceSelector:
    names:
      - "app-cluster01/bookinfo"
      - "app-cluster02/bookinfo"
```
### Fields
`spec`: contents are comparable to [YAML API Reference for TCTL](https://docs.tetrate.io/service-bridge/latest/en-us/reference/yaml-api)

### Annotations
Hierarchy information must be provided with the following annotations, where appropriate
- tsb.tetrate.io/organization
- tsb.tetrate.io/tenant
- tsb.tetrate.io/workspace
- tsb.tetrate.io/trafficGroup
- tsb.tetrate.io/securityGroup
- tsb.tetrate.io/gatewayGroup
- tsb.tetrate.io/istioInternalGroup
- tsb.tetrate.io/application

### kubectl
Once `kubectl apply` of the resource is done, can use familiar `kubectl` commands to check the created resource

```bash
kubectl get workspace -n bookinfo
NAME                 PRIVILEGED   TENANT   AGE
bookinfo-workspace                dev      10s
```