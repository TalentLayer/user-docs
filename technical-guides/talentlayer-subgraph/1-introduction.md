# Introduction

Welcome to the TalentLayer API documentation. This documentation is intended to help you get started with the TalentLayer API. It is a work in progress and will be updated regularly.

TalentLayer provides querying mechanisms by using the tools provided by [The Graph](https://thegraph.com/en/). The [TalentLayer Subgraph](https://github.com/TalentLayer/talentlayer-id-subgraph) is the implementation of [The Graph](https://thegraph.com/en/) that should be used to query TalentLayer data. The Data that can be queried is defined by [the Subgraph Schema](https://github.com/TalentLayer/talentlayer-id-subgraph/blob/main/schema.graphql) and can be explored using [the GraphQL explorer](https://cloud.hasura.io/public/graphiql).

<br>

---

<br>

## **Exploring the Subgraph**

**Subgraph link**

- [**Polygon Mumbai Testnet**](https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-mumbai)

- [**Polygon mainnet**](https://api.thegraph.com/subgraphs/name/talentlayer/talentlayer-polygon)

**Playground Link**

To ensure that your queries are working properly before using them in your project, you can use the Graph playgroun below.

- [**Polygon Mumbai playground**](https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-mumbai)

- [**Polygon mainnet pLayground**](https://thegraph.com/hosted-service/subgraph/talentlayer/talentlayer-polygon)

Please check the demo video just below <br>
[how test queries with The Graph Playground](https://loom.com/share/a95f65ebe9da4bd1908ca6aacf0b765b)

<br>

---

<br>

## **Using the Playground**

Using the playground you can create and save your own graphQL queries, as well as **try out the default queries that we provide to get you up and running!**

On the righthand side, you have access to some neat functionality that will help you explore the subgraph. Check out **the GraphQL Explorer** as well as **Documentation Explorer** to create customized queries on the fly!

<br>

## **An Introduction to Writing GraphQL Queries for the TalentLayer Subgraph**

The most commonly used entities has a related description entity that stores the off-chain data hosted on [IPFS](https://www.ipfs.com/).

| On-chain Entity | Off-chain Entity    |
| --------------- | ------------------- |
| Service         | ServiceDescription  |
| Proposal        | ProposalDescription |
| Review          | ReviewDescription   |
| User            | UserDescription     |
| Platform        | PlatformDescription |

The off-chain entity that is related to an on-chain entity can be accessed through the field description. Here is an example of what the relationship looks like in GraphQL.

```graphql
{
  services {
    id
    description {
      id
    }
  }
}
```

{% hint style="info" %}
This same pattern can be applied to the other entities by simply changing **services** to either **users, proposals, reviews,** or **platforms.**
{% endhint %}

<br>

> We will see more examples of this how build different queries in the queries example section.
