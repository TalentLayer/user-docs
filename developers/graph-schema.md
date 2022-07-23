# Graph Schema

## TalentLayer ID Subgraph

The TalentLayer Id Subgraph is hosted with [The Graph](https://thegraph.com/en/).

## Interacting with the Schema

The TalentLayer ID Schema can be interacted with via the following URL.

Query URL: [https://api.thegraph.com/subgraphs/name/talentlayerid/talent-layer-id](https://api.thegraph.com/subgraphs/name/talentlayerid/talent-layer-id)

## Schema

```graphql
type Job @entity {
  id: ID!
  employerId: BigInt!
  employeeId: BigInt!
  initiatorId: BigInt!
  jobDataUri: String
}

type Review @entity {
  id: ID! # totalSupply (unique id)
  jobId: BigInt!
  toId: BigInt!
  reviewUri: String!
}

type User @entity {
  id: ID!
  userTokenId: BigInt!
  handle: String!
  withPoh: Boolean!
}
```





