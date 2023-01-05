---
title: TSB Concepts
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: 0
tags: [Featured, TSB Concepts]
updated: 2022-12-07
category: TSB Concepts
intro:
  TSB Concepts Collection
---

## Intro

As you set out on your journey with [`Tetrate Service Bridge (TSB)`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/terminology#how-does-tsb-work), it's essential for you to understand its architecture, and how it's going to work within your environment.

## Resources

### Service Mesh Introduction

The Service Mesh architecture is being widely adopted today, and the team at Tetrate is made up of some of the earliest engineers building the technologies that enable the architecture. In this page we'll introduce the architecture and terminology, outline the capabilities and features, and discuss Istio - the leading mesh implementation and the service mesh that powers Tetrate Service Bridge. [`Service Mesh Introduction`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/service_mesh)

### Architecture

The previous section covered what a service mesh is, and introduced Istio — the service mesh that powers Tetrate Service Bridge. This section is all about the architecture that makes up TSB. [`Architecture`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/architecture)

### Security

Security is integrated into every part of TSB, and zero trust is the basis for all security within your mesh-managed environment. TSB offers unique security advantages derived from smart user controls, and hardened access policies that you map to your organization's structure. TSB helps to protect your applications, support compliance efforts, by making it easier to manage resources, and prevent outages. [`Security`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/security) 

### Traffic Management

TSB's traffic routing capabilities let you easily control traffic flow between services under its control. TSB simplifies the approach to structuring how you interact with applications and services, and by extension, simplifies the processes behind tasks such as traffic routing, staged rollouts, and migrations. [`Traffic Management`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/traffic_management) 

### Global Observability

One of the most powerful benefits of the service mesh is providing consistent operational metrics (RED - Rate, Error, Duration), logging across every application in the mesh, and facilitating distributed tracing. However, when it comes to managing a service mesh across an organization's entire infrastructure, you're left to your own devices to piece together a view of the entire world for application developers and security owners. [`Global Observability`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/observability) 

### Configuration Data Flow

We described the layers that make up TSB in in the Architecture section: the data plane, local control planes, global control plane, and management plane. The data plane — Envoy — is managed by the local control plane — Istio and XCP Edge — and those local control planes are coordinated by the global control plane — XCP Central. Users author configuration through the management plane — TSB — and TSB pushes that configuration to XCP Central, and so on down the layers until the data planes enact that user configuration. [`Configuration Data Flow`](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/configuration-dataflow) 

### GitOps

The main idea behind the GitOps support in TSB is allowing application teams to create TSB configuration resources directly in the application clusters. This allows them to push changes to application configuration the same way they push changes to the applications themselves, and allows packaging together the application deployment resources and the TSB configurations, for example inside the same Helm chart. [`GitOps`](https://docs.tetrate.io/service-bridge/1.5.x/en-us/howto/gitops) 