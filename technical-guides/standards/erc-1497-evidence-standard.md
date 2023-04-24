# ERC-1497: Evidence Standard

## About The Standard

{% embed url="https://github.com/ethereum/EIPs/issues/1497" %}

Defines a standard for submitting evidence in dispute resolution. Evidence is not stored on-chain due to gas considerations. Instead it is represented with off-chain resources, standardized JSON objects that can be hosted anywhere.

Evidence are submitted and looked up via smart contract event logs. We can leverage the immutability and availability of the blockchain to create a permanent log of submission that any interface can look up and use to access the evidence JSON.

It defines a standard way for dApps that are part of the dispute resolution process to share context and information:

* for Arbitrable dApps: gives a way to provide the details of disputes to the Arbitrator.
* for Arbitrators: gives a way to see context and evidence of disputes that need to be ruled.



### `Evidence`

Material provided by each party of a dispute in order to support their viewpoint, submit extra information for arbitrators and give reasons why they believe they are right.

It’s extra information that parties can submit for arbitrators that tries to prove that the dispute should be ruled in favor.

E.g.: emails, screenshots, contracts, testimony

**How it’s used:**

* `Arbitrable` contracts emit an event that contains a reference to an evidence JSON file when new evidence is submitted.



### `MetaEvidence`

Gives context to a dispute so that arbitrators are able to accurately and fairly evaluate it. Used to convey general information about the dispute to the arbitrator.

E.g.: the agreement, parties involved, what has to be decided (the question the arbitrators have to answer), the human readable meanings of rulings and specific modes of display for evidence.

**How it’s used:**

* Each dispute includes only one piece of `MetaEvidence`, however, the same `MetaEvidence` can be used for multiple disputes
* It is up to the `Arbitrable`contract to determine how `MetaEvidence` is submitted and assigned to a dispute
* In some use cases, `MetaEvidence` is all that the `Arbitrator` will need in order to make a ruling.
* `MetaEvidence`has to be created before a dispute can arise. It should be created at the same time as the agreement so that it can be impartial.
