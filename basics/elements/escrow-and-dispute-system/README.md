# Escrow

The TalentLayer Escrow and Dispute Resolution Module allows for secure payments between users on TalentLayer integrated marketplaces AND between TalentLayer integrated marketplaces. TalentLayer's Escrow and Dispute Resolution allows for users on different marketplaces to remit transactions and handle disputes associated with [specific Services.](../jobs-and-proposals/)

The TalentLayer Escrow System is an adaptation of [Kleros's MultipleArbitrableTransaction.sol](https://github.com/kleros/kleros-interaction/blob/master/contracts/standard/arbitration/MultipleArbitrableTransaction.sol) smart contract and Yubiai's [MultipleArbitrableTransaction.sol](https://github.com/yubiai/yubiai-contracts/blob/main/contracts/MultipleArbitrableTransaction.sol) updated version.&#x20;

## Capabilities

It is possible for escrow to be released in part to the counter-party by the employer. This feature allows for things like milestone-based projects; where based on the delivery of certain sub-services, an employee can receive payments. This also enables periodical payment of hourly work; for example, weekly pay for hours worked.

Escrow contracts can not currently be refilled after the full amount has been released. After the full amount has been released, the service will automatically be marked complete and prompt the users to leave a review. Future transactions will have to be completed in a subsequent service.

It is possible for a freelancer to voluntarily opt-out of a service and be compensated partially for work completed, with the employer receiving the remaining amount of escrow back to their own wallet.

## TalentLayer Escrow With or Without Disputes

At the platform level, you can decide whether to allow your users to initiate disputes via Kleros or not. If you choose to allow for disputes via Kleros, handling of the release of escrow after a dispute has been judged is automatically completed by the contracts.

{% hint style="info" %}
**Alternative Dispute Resolution Protocols:** TalentLayer aims to eventually allow integrated platforms to interface easily with an array of decentralized dispute resolution protocols. Kleros is currently the industry leader in decentralized dispute resolution and was therefore an obvious first choice.
{% endhint %}

## Smart Contracts

The [**Kleros folder**](https://github.com/TalentLayer/talentlayer-id-contracts/tree/main/contracts/kleros) **** is the main parent folder of all contracts associated with Escrow and Dispute Resolution**.** These contracts facilitate the creation of custom escrow accounts for each instance of a job.

| Contract on Github                                                                                                                                                                | Use                                                                                                                                                                                                |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [TalentLayerArbitrator.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/TalentLayerArbitrator.sol)                                         | TalentLayerArbitrator contract initiates the judgment process for the TalentLayerMultipleArbitrableTransaction contracts. Arbitrator contracts give rulings and Arbitrable contracts enforce them. |
| [TalentLayerMultipleArbitrableTransaction.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/TalentLayerMultipleArbitrableTransaction.sol)   | This is the actual escrow contract - here all pertinent functions that must be called to manage escrow transactions can be found.                                                                  |
| [ITalentLayerMultipleArbitrableTransaction.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/ITalentLayerMultipleArbitrableTransaction.sol) | Arbitrator Interface contract for TalentLayerMultipleArbitrableTransaction.sol                                                                                                                     |
| [Arbitrable.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/Arbitrable.sol)                                                               | A standard contract that can be judged against by an Arbitrator contract.                                                                                                                          |
| [Arbitrator.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/Arbitrator.sol)                                                               | Arbitrator contracts initiate the judgment process for Arbitrable contracts. Arbitrator contracts give rulings and Arbitrable contracts enforce them.                                              |
| [IArbitrable.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/IArbitrable.sol)                                                             | Arbitrator Interface contract.                                                                                                                                                                     |
