# Arbitration

## Arbitration of Escrow

We have an escrow that allows to perform transactions between two parties (seller and buyer of a service). Seller and buyer can create disputes.

The escrow can be ruled by an arbitrator, which will have the power to decide where the funds will go in case of a dispute (either pay the seller or reimburse the buyer).

The contract follows the `Arbitrable` standard.

{% hint style="info" %}
The initial implementation offers only a binary decision where one user receives 100% of the pay-out after a ruling. We ideally don’t want this to be a binary decision, but instead allow to release part of the funds to one party and some to another one (e.g. 50% - 50%). We intend to adapt this.
{% endhint %}

## **Arbitrator Options**

We intend to offer support for various decentralized dispute resolution options. The goal is to have Arbitration be as modular as possible.&#x20;

### Kleros Arbitration

Currently, we support Kleros, which is a dispute protocol with a network of jurors that act as the arbitrator for disputes. Kleros only supports disputes on the Ethereum blockchain.&#x20;

### Platform-Managed Arbitration

Since Kleros doesn’t exist on all chains, we need an alternative solution for these other chains. For now, we provide a centralized solution "Platform-Managed Arbitration" where platforms have the power to rule on the disputes which arise on services created with them. This is conducted similar to how most marketplaces handle disputes today - with customer service agents or administrators deciding rulings.

{% hint style="info" %}
The initial implementation has no appeals. We plan to implement appeals.&#x20;
{% endhint %}

The contract will follow the `Arbitrator` standard.

[TalentLayerArbitrator.sol](https://www.notion.so/TalentLayerArbitrator-sol-569f042d393a40d8a531eff0e61a938e)

Where multiple options for arbitration are available, for example, on Ethereum, the platform can choose which solution they want to support (either Kleros, or platform-managed, etc..)
