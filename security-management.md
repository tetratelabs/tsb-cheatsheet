---
title: Security Settings Management
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: Resources
intro:
  <a href='https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/security/v2/yaml'>Security Settings Management</a> in TSB.
---

## Intro

### Resources
- SecurityGroup allow grouping the proxy workloads in a set of namespaces owned by its parent workspace
- [`SecuritySetting`](#securitysetting) allows configuring security related properties such as TLS authentication and access control for traffic arriving at a proxy workload in a security group

### tsb/security/v2

- [SecurityGroup](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/security/v2/security_group)
- [SecuritySetting](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/security/v2/security_setting)

## SecuritySetting

### Sample

#### sample/traffic-management/securitysetting.yaml

```yaml
---
apiVersion: security.tsb.tetrate.io/v2
kind: SecuritySetting
metadata:
  organization: tsbdemo
  tenant: bookinfo
  workspace: bookinfo-workspace
  group: bookinfo-securitygroup
  name: bookinfo-sg
spec:
  authenticationSettings:
    trafficMode: REQUIRED
```

### Fields

Interpretations of fields in the sample
- `authenticationSettings`: Defines if mTLS is required to be enabled or not