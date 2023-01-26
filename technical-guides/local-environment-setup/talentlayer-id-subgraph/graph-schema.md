# Graph & Endpoints

The TalentLayer Subgraph is hosted on [The Graph](https://thegraph.com/en/)'s decentralized managed hosting service. In mid-2023 we will be migrating to their decentralized hosting service.

## Reading from TalentLayer

TalentLayer is multi-chain. Each platform must choose at least one TalentLayer Core chain implementation to read from.

Reading is necessary to display repetitional and service information on your UI. You can create features such as:

* Reputation search pages
* Service search pages
* Pages that show a user their own reputation
* More

There are three key **data entities** that can be searched in the TalentLayer Graph:

1. Service - A service that has been minted and it’s status
2. User - A user’s TalentLayer ID NFT
3. Review - A review that has been minted and associated with someone’s TalentLayer ID

The TalentLayer Graph is highly flexible: you can query and sort many diverse data points on services, reputations, identities, and how they associate with one another.

## Exploring the Schema

The [TalentLayer Graph Schema ](https://github.com/TalentLayer/talentlayer-id-subgraph/blob/main/schema.graphql)can be tested, explored and query easly:&#x20;

* Using one of the official playground links that you can find bellow (example for Goerli: [https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-protocol](https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-protocol)).
* With the [the GraphQL explorer](https://cloud.hasura.io/public/graphiql) tool with any of the endpoints.
* By directly visiting the endpoint links and manually inputting the query.

| Blockchain              | Docs & Playground                                                                                                                                                | Endpoint                                                                                                                                               |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Ethereum Goerli Testnet | [https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-protocol](https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-protocol) | [https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol](https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol) |
| Avalanche Fuji Testnet  | [https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-fuji](https://thegraph.com/hosted-service/subgraph/talentlayer/talent-layer-fuji)         | [https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-fuji](https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-fuji)         |

## Querying the graph&#x20;

This is an example of a query that you can run:&#x20;

```
// Get last 5 opened services with their offchain data for the platform 1

{
  services(
    orderBy: createdAt,
    orderDirection: desc,
    first: 5,
    where: {
      status: Opened,
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
      id, 
      handle, 
      numReviews,
    }
    description {
      id,
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
