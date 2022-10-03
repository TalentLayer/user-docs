# Escrow & Disputes

The /**Kleros folder is the main parent folder of all contracts associated with Escrow and Dispute Resolution.**  These contracts facilitate the creation of custom escrow accounts for each instance of a job.

| Contract on Github                                                                                                                                                                | Use                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [TalentLayerArbitrator.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/TalentLayerArbitrator.sol)                                         | TalentLayerArbitrator contract initiates the judgment process for the TalentLayerMultipleArbitrableTransaction contracts. Arbitrator contracts give rulings and Arbitrable contracts enforce them.  |
| [TalentLayerMultipleArbitrableTransaction.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/TalentLayerMultipleArbitrableTransaction.sol)   | This is the actual escrow contract - here all pertinent functions that must be called to manage escrow transactions can be found.                                                                   |
| [ITalentLayerMultipleArbitrableTransaction.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/ITalentLayerMultipleArbitrableTransaction.sol) | Arbitrator Interface contract for TalentLayerMultipleArbitrableTransaction.sol                                                                                                                      |
| [Arbitrable.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/Arbitrable.sol)                                                               | A standard contract that can be judged against by an Arbitrator contract.                                                                                                                           |
| [Arbitrator.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/Arbitrator.sol)                                                               | Arbitrator contracts initiate the judgment process for Arbitrable contracts. Arbitrator contracts give rulings and Arbitrable contracts enforce them.                                               |
| [IArbitrable.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/IArbitrable.sol)                                                             | Arbitrator Interface contract.                                                                                                                                                                      |

### Explore the Kleros Documentation

TalentLayer Escrow is based on a fork of Kleros escrow. Kleros escrow is an escrow system that natively interfaces with the Kleros Court arbitration system - allowing court decisions to automatically facilitate the release of escrow to the winning party. TalentLayer Escrow was designed with special features to allow it to connect with the TalentLayer Job Registry and inform reviews left via the TalentLayer Review System.&#x20;

{% embed url="https://kleros.gitbook.io/docs/products/escrow/kleros-escrow-specifications" %}

{% embed url="https://kleros.gitbook.io/docs/developer/arbitration-development/erc-792-arbitration-standard" %}

{% embed url="https://kleros.gitbook.io/docs/developer/arbitration-development/erc-1497-evidence-standard" %}

### Explore How Jobs and Proposals Can Meet Your Platform's Needs

With milestone-based payments, partial payments, and more configurations, TalentLayer Escrow helps your platform meet your user's needs.&#x20;

{% content-ref url="../../work-facilitation-module/escrow-and-dispute-system.md" %}
[escrow-and-dispute-system.md](../../work-facilitation-module/escrow-and-dispute-system.md)
{% endcontent-ref %}

### View on Github

{% embed url="https://github.com/TalentLayer/talentlayer-id-contracts/tree/main/contracts/kleros" %}
