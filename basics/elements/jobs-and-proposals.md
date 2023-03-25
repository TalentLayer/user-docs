# Services

[TalentLayerService.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerService.sol) is the smart contract that creates an instance of a Services and associates Proposals with that service as they are submitted. Services and Proposals are not minted as NFTs - rather, their data are stored in an on-chain registry within the smart contract and on IPFS for detailed informations. Services and Proposals updated easily depending on their status.

The Service Registry is a searchable on-chain repository of services such as jobs that can be posted to and read from by any integrated platform. This cross-posting allows for a broader range of users to view and submit proposals for a wide range of services.

The Service Registry contains a few sub-components that can be used together or separately based on the goals of your platform.

## Services

Services are created by Users on TalentLayer-integrated platforms. Services' metadata is stored in the ServiceRegistry.sol smart contract and on IPFS. Services are viewed on platforms by searching the TalentLayer Graph based on keywords, geographic origins, service types, and other factors.

### Service Status

&#x20;are assigned different statuses based on the stage of the service lifecycle they are in.

```
enum Status {
    Opened /// The service has been created, but not assigned to an employee yet
    Confirmed, /// The service has been consented to by an employee
    Finished, /// The service has been market completed by an employer
    Cancelled, /// The service has been canceled by the employer
    Uncompleted, /// The service
}
```

## Proposals

Services with Proposals are executable across multiple platforms.

For example, User A, the employer can post a Service on Platform Y and User B can search for and submit a Proposal for that Service on Platform Z.

When a proposal is created by a user for a service, the proposal is stored in an array inside the metadata of that service.

A proposal is automatically marked as validated when the employer sends the money to the escrow.

Then on every release of money to the worker, platform Y and platform Z will have percentage fees on it depending on their own configuration.

## Learn More About The Tech

Learn more about the technical side of services and proposals in our Technical Guide on the smart contract.&#x20;

{% content-ref url="../../technical-guides/smart-contracts/talentlayerservice.sol.md" %}
[talentlayerservice.sol.md](../../technical-guides/smart-contracts/talentlayerservice.sol.md)
{% endcontent-ref %}
