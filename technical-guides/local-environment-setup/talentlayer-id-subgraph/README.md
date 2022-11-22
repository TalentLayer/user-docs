---
description: Guide to setup subgraph on localhost.
---

# Talentlayer-id-subgraph

{% hint style="info" %}
First you must complete the steps in [Talentlayer-id-contracts](../talentlayer-id-contracts.md)
{% endhint %}

## Requirements

[The Graph CLI](https://thegraph.com/en/). Installation instructions found [here](https://thegraph.com/docs/en/deploying/deploying-a-subgraph-to-studio/#installing-graph-cli).

[Docker](https://www.docker.com/). Installation instructions found [here](https://docs.docker.com/get-docker/).

## Instructions

### 1. Clone Repository from GitHub

```bash
git clone https://github.com/TalentLayer/talentlayer-id-subgraph
```

### 2. Navigate to Folder

```bash
cd talentlayer-id-subgraph
```

### 3. Start Subgraph Node

{% hint style="info" %}
Make sure Docker is running.
{% endhint %}

```bash
sh run-graph-node.sh
```

### 4. Deploy Subgraph To Node

```bash
make regenerate
```
