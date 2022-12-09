---
title: TSB Terminology
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: 0
tags: [Featured]
updated: 2022-12-07
category: Concepts
intro:
  A handy list of terms used when describing TSB and its environment.

---

## Intro

A handy list of terms used when describing TSB and its environment.

## Tetrate Service Bridge

### Tetrate Service Bridge (TSB)
TSB is a service mesh management plane that's designed to provide you with a
single place to manage your entire infrastructure. It maps to your existing
organizational structure, and enables you to provision access rights according
to your already established teams and needs.

More details can be found in the [TSB Architecture](https://docs.tetrate.io/service-bridge/latest/en-us/concepts/architecture) page.

### Organization
In TSB, an organization is the name we give to the corporation that has a shared
infrastructure, and manages all the individual teams within that corporation.

### Tenant
A tenant is a group within an organization *(e.g. a team or department)* who
shares organizational resources, and common access to resources with specific
privileges *(including read, write)*.

### Workspace
A workspace is a strictly partitioned zone where teams manage their 
exclusively-owned namespaces. It maintains all service mesh-related
configurations associated with that team's namespaces across any number of
Virtual Machines and Kubernetes clusters.

### Service
A network servable/addressable destination that is identifiable and 
independently authenticated.

### Group
A logical grouping of resources under a Workspace. A group may be one
of [gateway](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/gateway/v2/gateway_group/), [traffic](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/traffic/v2/traffic_group/), or [security](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/security/v2/security_group/) group.

### Application
A logical grouping of Services that expose a set of APIs that can be consumed
by end-users or other services. Applications are scoped to a Tenant and configure
how the different services they contain can be consumed and observed.

They provide a developer-centric experience when it comes to configuring how services
behave and the conditions that need to be enforced when accessing them.

### Application API
A set of endpoints serving features that are exposed by an Application. APIs provide
a developer-centric experience and allow configuring the Application Ingress gateways
with standard [OpenAPI documents](https://www.openapis.org/). This provides an abstraction
that is agnostic of the infrastructure that developers can leverage to configure their
applications and services without having to be exposed to the details of the underlying
compute and networking technologies.

### User
A user models an entity in TSB - both humans and a non-person entities. They can be grouped into [Teams](#team). Users can be assigned access to resources with [TSB's RBAC API](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/rbac/v2/yaml/) just like Teams. You can create and manage Users in TSB manually via the [Users and Teams API](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/v2/team/), but in most cases [TSB syncs Users and Teams from your source of truth](./security.mdx#user-access-policies) at a regular interval (configured during TSB installation).

### Team
A team is a group of [Users](#user), and acts as a handle for assigning many users access to resources with [TSB's RBAC API](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/rbac/v2/policy_service). We recommend always assigning teams, never individuals, access in TSB as a security best practice. You can create and manage Teams in TSB manually via the [Users and Teams API](https://docs.tetrate.io/service-bridge/latest/en-us/refs/tsb/v2/team), but in most cases [TSB syncs Users and Teams from your source of truth](./security.mdx#user_management_access_policies) at a regular interval (configured during TSB installation).

## Architectural Components

### Management Plane
The TSB management plane is your primary access point to everything within your
environment. It's your one place to configure networking, security, and 
observability using the UI or CLI to make updates and changes.  It provides
centralized control in a multi control plane service mesh.

More information can be found in the [TSB Architecture](./architecture) page.

### Global Control Plane / XCP
The global control plane is part of the management plane. It's concerned with
the literal state of your mesh-managed system as a whole, and holds the state of
the entire ecosystem under the control of TSB. It provides multi-cluster
features on top of the different local control planes.

More information can be found in the [TSB Architecture](./architecture) page.

### Control Plane
The local control plane is an Istio service mesh that is deployed in every 
cluster to create isolated failure domains between clusters. It allows TSB to
make use of all the features of Istio, including enforcing mTLS between
applications, as well as making intelligent networking and traffic routing
decisions between microservices within each cluster.

More information can be found in the [TSB Architecture](./architecture) page.

### Data Plane
Powered by Envoy, the data plane enables data transfer between services using
‘sidecars' that sit next to microservices and send and receive data on behalf of
the applications.

More information can be found in the [TSB Architecture](./architecture) page.

### Sidecar Proxy
A instance of Envoy deployed beside an instance of your application as part of the mesh. It intercepts all traffic into and out of the application, allowing the service mesh to implement its traffic management, security, and observability features. This is in contrast to a [Load Balance](#load_balancer) or [Gateway](#gateway) which are deployed separately from your application.

In these docs we'll often shorten "sidecar proxy" to just **sidecar**.

### Load balancer
A load balancer sits in front of your servers and distributes requests based on
availability and capacity.

### Gateway
A gateway describes a load balancer operating at the edge of a mesh receiving
incoming or outgoing HTTP/TCP connections. In a multi-cluster TSB ecosystem we
distinguish between the following types of gateways:

- **Application Edge Gateway** (also called a "Tier 1 Gateway") distributes traffic across one or more ingress gateways in other clusters over Istio mTLS. This will be the entry point to the TSB service mesh which is spanning over multiple clusters.
- **Application Ingress Gateway** (also called a "Tier 2 Gateway") distributes traffic to one or more workloads (business application services) running in the cluster. The source of the traffic could be:
    1. an Edge Gateway: communicating over Istio mTLS. Then the mesh started at that Edge Gateway.
    2. a Client on the internet (outside TSB). Then the mesh starts at this Ingress Gateway.
    3. a service running on another cluster in TSB. Then the mesh entrypoint will be an Ingress Gateway or sidecar on the remote cluster.
- **Egress Gateway** provides a gateway for traffic originating from one or more
  workloads (business application services) running in the cluster to external services outside the mesh.
- **VM Gateway** provides a gateway for traffic originating from onboarded VMs
  to route correctly to other mesh workloads.

### Service Registry
The service registry is a central point where you can see a list of every
service that exists in the TSB platform's onboarded clusters.

### Front Envoy (Envoy Gateway)
The [Envoy](#envoy) gateway that accepts incoming traffic to TSB components, e.g. API calls, commands from `tctl`, communications to clusters managed by TSB (i.e. Global Control Plane)

## Other Terminology

### Kubernetes
Your guess is as good as mine… But here is an
[overview](https://kubernetes.io/docs/concepts/overview/) on the Kubernetes
site.

### Cluster
A [cluster](https://kubernetes.io/docs/reference/glossary/?all=true#term-cluster)
is a set of compute nodes. A node can contain Kubernetes pods, VMs, Bare Metal,
or a combination of all three if they share a trust domain.

### Namespace
[Namespaces](https://kubernetes.io/docs/reference/glossary/?all=true#term-namespace) are used in Kubernetes to group resources (e.g. containers, pods or nodes) into a logical grouping. By default all resources in Kubernetes belong to the "default" namespace. TSB resources typically are grouped into the "tsb" namespace.

### Failure Domain
A physical or logical section of your environment that is negatively affected, or likely to fail when a critical device or service experiences problems.

### Silo
A set of failure domains that are aligned together into a single unit that can be reasoned about and replicated for availability.

### Availability Zone
An isolated location within a cloud provider's [Region](#region) to deploy infrastructure resources like compute, storage, and networking. These represent a set of infrastructure failure domains from the cloud provider's point of view. It's not uncommon that multiple availability zones in the same region can have correlated failure modes - i.e. go down together. To build reliable applications we certainly need to deploy in multiple availability zones, and often across multiple regions too.

### Region
A set of physical locations -- typically one or more data centers -- that represent a set of failure domains for a cloud provider. These are typically subdivided into [availability zones](#availability_zone) which are the unit you actually interact with.

## OSS Projects

### Istio
Istio is an open source service mesh that provides a transparent and
language-independent way to flexibly and easily automate application network
functions. To learn more about Istio's capabilities, visit the
[Istio](https://istio.io/) website.

### Envoy
Envoy is an [L7](https://en.wikipedia.org/wiki/OSI_model#Layer_7:_Application_Layer)
proxy and communications system designed for large modern service oriented
architectures. All of the Envoys form a transparent communication mesh in which
each application sends and receives messages to and from localhost and is
unaware of the network topology. To learn more about Envoy, visit the [Envoy
Proxy](http://envoyproxy.io/) website.

### SkyWalking
Apache SkyWalking is an Observability Application Platform (OAP) and Application
Performance Monitor (APM) tool that includes distributed tracing, service mesh
telemetry analysis and metrics aggregation to provide you with a full image of
the health of your services and service mesh. For more information, visit the
[Apache SkyWalking](https://skywalking.apache.org/) website.

### Next Generation Access Control (NGAC)
[Next Generation Access Control](https://www.nist.gov/topics/identity-access-management/policy-machine-and-next-generation-access-control), NGAC, is a cutting-edge access control system developed by NIST and Tetrate under a collaborative research agreement. It's a *graph based* take on traditional Attribute Based Access Control (ABAC) with better runtime performance, flexible model, and first-class primitives for understanding the effects of a policy change with notions of Audit (who did what when) and Explain (why was an action allowed/disallowed in semantic terms) designed into the specification.me Helm chart.