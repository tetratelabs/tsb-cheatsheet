---
title: TSB Quickstart
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: +1
tags: [Featured, TSB Quickstart]
updated: 2022-12-07
category: Quickstart
intro:
  TSB Quickstart Collection
---

## Intro

The [`Quickstart`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/introduction)  is written to walk you through application onboarding and configuration of your application on TSB. By reading the quickstart, you are going to learn how to deploy your application and how to configure TSB and its components for various basic scenarios.


## Resources

- [`Deploy an Application`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/deploy_sample_app) In this quickstart page, you're going to deploy a sample application in a demo TSB environment and validate the success using the TSB UI, and tctl commands.
- [`Create a Tenant`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/tenant) In this section, you're going to create a Tenant within TSB.
- [`Create a Workspace`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/workspace) In this section, you're going to create a Workspace called `bookinfo-ws` bound to the `bookinfo` namespace.
- [`Create Config Groups`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/config_groups) To start configuration for the bookinfo application, create a Gateway Group, a Traffic Group, and a Security Group. Each group provides specific APIs to configure various aspects of the services.
- [`Configuring RBAC Permissions`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/permissions) In this scenario, you will use the different AccessBindings to configure two RBAC access policies.
- [`Ingress Gateway`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/ingress_gateway) In this scenario, you'll use a Gateway to allow external traffic to your bookinfo application.
- [`Traffic Shifting`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/traffic_shifting) In this scenario, you will use a Service Route to shift traffic from the reviews v1 to reviews v2 service.
- [`Security`](https://docs.tetrate.io/service-bridge/latest/en-us/quickstart/security) In this scenario, you'll configure communication between services in the same workspace using TSB security settings.
