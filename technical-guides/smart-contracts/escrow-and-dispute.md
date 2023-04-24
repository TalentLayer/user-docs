# Escrow & Dispute Contracts

[**TalentLayerEscrow.sol**](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerEscrow.sol) is the smart contract that handles escrow transactions for each service, it custody the money and allow hirer to release the money by milestone. Also, in case of a dispute it handle all the workflow and link with the configured arbitrator.&#x20;

It can used to:

* Validate a proposal for a given service and deposit the money
* Release money for the worker&#x20;
* Let the worker reimburse the hirer
* Raise a dispute
* As a platform, claim the fees earned

## Data Structure

![](<../../.gitbook/assets/image (4).png>)

## Visualization: TalentLayerEscrow.sol

<figure><img src="../../.gitbook/assets/escrow.svg" alt=""><figcaption></figcaption></figure>

## Visualization: TalentLayerArbitrator.sol

<figure><img src="../../.gitbook/assets/arbitrator.svg" alt=""><figcaption></figcaption></figure>

## Learn More

Learn more about our escrow and dispute system and how they function in workflows:&#x20;

{% content-ref url="escrow-and-dispute/" %}
[escrow-and-dispute](escrow-and-dispute/)
{% endcontent-ref %}
