---
title: tctl CLI
layout: 2017/sheet
prism_languages: [bash,yaml]
weight: -3
tags: [Featured]
updated: 2022-12-07
category: CLI
intro: 
  tctl cli
---

## TCTL

### Quicklinks

- [Getting Started](https://docs.tetrate.io/service-bridge/latest/en-us/reference/cli/guide/index)
- [Download tctl](https://binaries.dl.tetrate.io/public/raw/)
- [Reference](https://docs.tetrate.io/service-bridge/latest/en-us/reference/cli/reference)

## Setup

### config

The `config` command will setup a profile to interact with TSB

Example
```bash
# Configure Cluster
tctl config clusters set ${TSB_CLUSTER_NAME} --bridge-address ${TSB_ADDRESS}

# Setup User Credentials for Cluster
tctl config users set ${USERNAME}-${TSB_CLUSTER_NAME} --org tetrate --username ${USERNAME} --password ${PASSWORD} --tenant ${TENANT} --org ${ORG}

# Cluster and User Binding
tctl config profiles set ${TSB_CLUSTER_NAME}-profile --cluster ${TSB_CLUSTER_NAME} --username ${USERNAME}-${TSB_CLUSTER_NAME}

# Set default profile
tctl config profiles set-current ${TSB_CLUSTER_NAME}-profile
```

### login

```bash
# Login to TSB under specific tenant
tctl login --org tetrate --tenant dev
```

### version

```bash
# obtain version of tctl and tsb
tctl version
```

### completion

The `completion` will build tab completion scripts

```bash
# Bash Example
source <(tctl completion bash)

# Zsh Example
tctl completion zsh > "${fpath[1]}/_tctl"
```

## TSB Configuration

### get

The `get` command can retreive configuration from TSB

```bash
# List all clusters onboarded to TSB
tctl get clusters

# List of synced users
tctl get users

# Search all resources of kind Tier1gateway for specific tenant
tctl get all --kind Tier1Gateway --tenant tier1

# List all GatewayGroups under specific workspace
tctl get --workspace bookinfo-ws GatewayGroup --tenant tetrate 

# Display GatewayGroup configuration under specific workspace
tctl get all --workspace bookinfo-ws --gatewaygroup bookinfo-gg --tenant tetrate 
```

### edit

The `edit` command can edit configuration in TSB

```bash
# Setup EDITOR env variable
EDITOR=vim

# Edit gatewaygroup
tctl edit gatewaygroup --workspace bookinfo-ws --gatewaygroup bookinfo-gg
```

### apply

The `apply` command allows user to push configuration to TSB

```bash
# Edit gatewaygroup
tctl apply -f bookinfo-gg.yaml
```

### status

The `status` command will provide status of objects applied to TSB

```bash
# Get status of a cluster
tctl x status cluster dev-canadaeast-1

# Get status of a configured workspace 
tctl experimental status workspace bookinfo-ws --tenant bookinfo

# Get status of a configured IngressGateway
tctl x status ingressgateway bookinfo-productpage --tenant bookinfo --workspace bookinfo-ws --gatewaygroup bookinfo-gg
```

## Install
### install

The `install` command can be used to get TSB setup and onboard clusters

```bash
# Sync Tetrate images with private registry
tctl install image-sync --username ${USERNAME} --apikey ${API_TOKEN} --registry ${PRIVATE_REGISTRY}

# Obtain a list of TSB images
tctl install image-sync --accept-eula --just-print

# Setup ServiceAccount and obtain JWK for new Cluster Onboarding
tctl install cluster-service-account --cluster ${CLUSTER} > cluster-${CLUSTER}-service-account.jwk

```
