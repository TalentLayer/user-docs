# Job Registry

**JobRegistry.sol** is the smart contract that creates an instance of a job. Jobs are not minted as NFTs - rather, their data is stored in an on-chain registry within the smart contract. Jobs can be deleted or updated easily.&#x20;

It can be broken up into a few parts:&#x20;

* Creation of a job and the tagging of a counterparty for the job
* Agreement to the job by the counterparty or Rejection
* Finalization of job

### View on Github

{% embed url="https://github.com/TalentLayer/talentlayer-id-contracts" %}
