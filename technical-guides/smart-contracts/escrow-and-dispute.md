# Escrow & Dispute Contracts

## Contracts

All contracts associated with Escrow and Dispute Resolution are available in their parent folder here:&#x20;

{% embed url="https://github.com/TalentLayer/talentlayer-id-contracts/tree/main/contracts/kleros" %}

| Contract on Github                                                                                                                                                                | Use                                                                                                                                                                                                |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [TalentLayerArbitrator.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/TalentLayerArbitrator.sol)                                         | TalentLayerArbitrator contract initiates the judgment process for the TalentLayerMultipleArbitrableTransaction contracts. Arbitrator contracts give rulings and Arbitrable contracts enforce them. |
| [TalentLayerMultipleArbitrableTransaction.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/TalentLayerMultipleArbitrableTransaction.sol)   | This is the actual escrow contract - here all pertinent functions that must be called to manage escrow transactions can be found.                                                                  |
| [ITalentLayerMultipleArbitrableTransaction.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/ITalentLayerMultipleArbitrableTransaction.sol) | Arbitrator Interface contract for TalentLayerMultipleArbitrableTransaction.sol                                                                                                                     |
| [Arbitrable.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/Arbitrable.sol)                                                               | A standard contract that can be judged against by an Arbitrator contract.                                                                                                                          |
| [Arbitrator.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/Arbitrator.sol)                                                               | Arbitrator contracts initiate the judgment process for Arbitrable contracts. Arbitrator contracts give rulings and Arbitrable contracts enforce them.                                              |
| [IArbitrable.sol](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/kleros/IArbitrable.sol)                                                             | Arbitrator Interface contract.                                                                                                                                                                     |

## Learn More

Learn more about our escrow and dispute system and how they function in workflows:&#x20;

{% content-ref url="escrow-and-dispute/" %}
[escrow-and-dispute](escrow-and-dispute/)
{% endcontent-ref %}
