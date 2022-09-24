# Graph Schema

## TalentLayer Subgraph

The TalentLayer Subgraph is hosted on [The Graph](https://thegraph.com/en/)'s decentralized managed hosting service. In late 2022 we will be migrating to our own hosting on FileCoin.

## Exploring the Schema

The TalentLayer Graph Schema can be explored via the following URLs.&#x20;

Explorer: [https://graphiql-online.com/](https://graphiql-online.com/)

| Blockchain              | Endpoint                                                                                                                                               |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Gnosis/xDAO             | [https://api.thegraph.com/subgraphs/name/talentlayerid/talent-layer-id](https://api.thegraph.com/subgraphs/name/talentlayerid/talent-layer-id)         |
| Ethereum Goerli Testnet | [https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol](https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol) |

TalentLayer's Graph can query and sort many diverse datapoints on jobs, reputations, identities, and how they associate with one another.&#x20;

## Querying the Schema

Use the following endpoint to query the schema.

GraphQL Endpoint URL: [https://api.thegraph.com/subgraphs/name/talentlayerid/talent-layer-id](https://api.thegraph.com/subgraphs/name/talentlayerid/talent-layer-id)

### Schema Components

```graphql
enum JobStatus {
  Filled,
  Confirmed,
  Finished,
  Rejected,
  Opened
}

enum ProposalStatus {
  Pending,
  Validated,
  Rejected
}

type Job @entity {
  id: ID! # job token id
  status: JobStatus! # job status
  employer: User # job employer
  employee: User # job employee
  sender: User # user that created the job (employer or employee)
  recipient: User # other participating user (employee or employer)
  uri: String # metadata URI of job
}

type Review @entity {
  id: ID! # review token id
  job: Job! # job this review is for
  to: User! # reviewed user
  uri: String! # metadata URI of review
}

type User @entity {
  id: ID! # user token id
  address: String! # wallet address of user
  uri: String! # metadata URI of profile
  handle: String! # handle of user
  withPoh: Boolean! # whether user has proof of identity
  numReviews: BigInt! # number of reviews user has received
  rating: BigDecimal! # average rating from reviews user has received
  reviews: [Review!] @derivedFrom(field: "to") # reviews of user
  employerJobs: [Job!] @derivedFrom(field: "employer") # jobs user is an employer for
  employeeJobs: [Job!] @derivedFrom(field: "employee") # jobs user is an employee for
}
```
