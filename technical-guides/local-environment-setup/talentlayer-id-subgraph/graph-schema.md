# The Graph

TalentLayer provides querying mechanisms by using the tools provided by [The Graph](https://thegraph.com/en/). The [TalentLayer Subgraph](https://github.com/TalentLayer/talentlayer-id-subgraph) is the implementation of [The Graph](https://thegraph.com/en/) that should be used to query TalentLayer data. The Data that can be queried is defined by [the Subgraph Schema](https://github.com/TalentLayer/talentlayer-id-subgraph/blob/main/schema.graphql) and can be explored using [the GraphQL explorer](https://cloud.hasura.io/public/graphiql).

## Exploring the Subgraph

The easiest way to explore the TalentLayer subgraph is to check out the Graph's playground environment. We currently have two subgraphs hosted there, one for the Ethereum goerli testnet and one for the Avalanche fuiji testnet.

* [**TalentLayer Subgraph Playground - Ethereum Goerli Testnet**](https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-protocol)
* [**TalentLayer Subgraph Playground - Polygon Mumbai Testnet**](https://api.thegraph.com/subgraphs/name/akugone/talentlayer-mumbai)
* [**TalentLayer Subgraph Playground - Avalanche Fuji Testnet**](https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-fuji)

## Using the Playground

Using the playground you can create and save your own graphQL queries, as well as **try out the default queries that we provide to get you up and running!**

On the righthand side, you have access to some neat functionality that will help you explore the subgraph. Check out **the GraphQL Explorer** as well as **Documentation Explorer** to create customized queries on the fly!

## An Introduction to Writing GraphQL Queries for the TalentLayer Subgraph

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

### Querying Services

#### Querying Services with their related description

Any of the attributes associated with the entities can be queried.&#x20;

```graphql
{
  services {
    id
    createdAt
    updatedAt
    description {
      id
      title
      about
    }
  }
}
```

#### Filtering Services Based On Different Attributes

Queries can also be ordered by and limited in number based on the values of different attributes.

```graphql
# Get last 5 opened services with their offchain data for the platform 1
{
  services(
    orderBy: createdAt
    orderDirection: desc
    first: 5
    where: {
      status: Opened
      platform: "1"
    })
  {
    id
    createdAt
    updatedAt
    status
    platform {
      id
    }
    buyer {
      id 
      handle 
      numReviews
    }
    description {
      id
      title
      about
      startDate
      expectedEndDate
      keywords_raw
      rateToken
      rateAmount
    }
  }
}
```

{% hint style="info" %}
For more information about sorting, pagination, and filtering please check out [The Graph GraphQL API documentation](https://thegraph.com/docs/en/querying/graphql-api/).
{% endhint %}

#### Fulltext Search for ServiceDescription

The TalentLayer Subgraph further offers a fulltext search feature that can be used to make more advanced text searches.&#x20;

The fulltext search allows using operators to query service descriptions based on text. For example, all the services that has a description that contains either  the word `hadhat` or the word `development` in the field `title` or in the field `keywords_raw` can be found using the followng query:

```graphql
{
  serviceDescriptionSearchRank(text: "hardhat | development") {
    title
    about
    keywords_raw
    service {
      id
    }
  }
}
```

{% hint style="info" %}
For more information on which operators are allowed and how to use them, please check out the Graph's [documentations on fulltext search queries](https://thegraph.com/docs/en/querying/graphql-api/#fulltext-search-queries).
{% endhint %}
