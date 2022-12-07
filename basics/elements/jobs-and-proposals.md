# Services

****[**ServiceRegistry.sol**](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/ServiceRegistry.sol) is the smart contract that creates an instance of a Services and associates Proposals with that service as they are submitted. Services and Proposals are not minted as NFTs - rather, their data is stored in an on-chain registry within the smart contract. Services and Proposals can be deleted or updated easily.

The Service Registry is a searchable on-chain repository of services such as jobs and bounties that can be posted to and read from by any integrated platform. This cross-posting allows for a broader range of users to view and submit proposals for a wide range of services.

The Service Registry contains a few sub-components that can be used together or separately based on the goals of your platform.

## Services

Services are created by Users on TalentLayer-integrated platforms. Services' metadata is stored in the ServiceRegistry.sol smart contract and on IPFS. Services are viewed on platforms by searching the TalentLayer Graph based on keywords, geographic origins, service types, and other factors.

### Service Status

&#x20;are assigned different statuses based on the stage of the service lifecycle they are in.

```
    enum Status {
        Filled, /// The service has been assigned to an employee
        Confirmed, /// The service has been consented to by an employee
        Finished, /// (if no escrow) The service has been market completed by an employer or (if escrow) escrow has been released 
        Rejected, /// The service has been removed by the employer
        Opened /// The service has been created, but not assigned to an employee
    }
```

## Proposals

The TalentLayer Work Facilitation Module can be implemented with or without proposals.

Both Services with Proposals and Services without Proposals are both executable across multiple platforms, as long as they are connected with the [TalentLayer Escrow System.](broken-reference)

For example, User A, the employer can post a Service on Platform Y and User B can search for and submit a Proposal for that Service on Platform Z.

When a proposal is created by a user for a service, the proposal is stored in an array inside the metadata of that service.

Up to 40 proposals can be active at one time for a service. An employer can reject proposals they do not want, thus allowing new proposals to be submitted.

### Services Without Proposals

Platforms may want to implement a workflow where users can create services without proposals if they want their users to be able to directly assign employees for a service, without receiving open proposals.

In this implementation, the employer defines factors like pay rate and terms, with no on-chain counter-proposals possible from the potential employee's end.

### Services With Proposals

Platforms may want to implement a workflow where users can create services with proposals if they want users to be able to post services and have potential employees submit proposals for those services.

In this implementation, the Proposal defines the final pay rate and terms. When the Proposal is accepted by the employer, those terms are accepted.
