---
title: Security Settings Management
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: Resources
intro:
  Security Settings Management
---

## Intro


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