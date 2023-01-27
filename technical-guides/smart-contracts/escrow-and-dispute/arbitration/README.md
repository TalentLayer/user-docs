# Arbitration

## Arbitration of Escrow

We have an escrow that allows to perform transactions between two parties (seller and buyer of a service). Seller and buyer can create disputes.

The escrow can be ruled by an arbitrator, which will have the power to decide where the funds will go in case of a dispute (either pay the seller or reimburse the buyer).

{% hint style="info" %}
The initial implementation offers only either a binary decision (one user receives 100% of the pay-out after a ruling), or a 50% - 50% resolution (funds are equally split between the two parties). We ideally want this to be more flexible, by instead allowing to release a specific percentage of the funds to one party and the rest to the other one (e.g. 25% - 75%). We intend to adapt this.
{% endhint %}

## **Arbitration Solutions**

We intend to offer support for various decentralized dispute resolution options. The goal is to have Arbitration be as modular as possible.&#x20;

### Kleros Arbitration

Currently, we support Kleros, which is a dispute protocol with a network of jurors that act as the arbitrator for disputes. Kleros only supports disputes on the Ethereum blockchain.&#x20;

{% content-ref url="../../../../basics/elements/escrow-and-dispute-system/disputes.md" %}
[disputes.md](../../../../basics/elements/escrow-and-dispute-system/disputes.md)
{% endcontent-ref %}

### Platform-Managed Arbitration

Since Kleros doesn’t exist on all chains, we need an alternative solution for these other chains. For now, we provide a centralized solution "Platform-Managed Arbitration" where platforms have the power to rule on the disputes which arise on services created with them. This is conducted similar to how most marketplaces handle disputes today - with customer service agents or administrators deciding rulings.

{% hint style="info" %}
The initial implementation has no appeals. We plan to implement appeals.&#x20;
{% endhint %}

{% content-ref url="../../../../basics/readme/escrow-and-dispute/arbitration/platform-managed-arbitration.md" %}
[platform-managed-arbitration.md](../../../../basics/readme/escrow-and-dispute/arbitration/platform-managed-arbitration.md)
{% endcontent-ref %}



Where multiple options for arbitration are available, for example, on Ethereum, the platform can choose which solution they want to support (either Kleros, or platform-managed, etc..).

## Arbitration Management and Customization

Each platform has the ability to choose a set of parameters to customize its arbitration strategy. This is currently possible by interacting with the smart contracts of the protocol. We intend to provide a frontend that platforms can use to easily manage arbitration.

### Updating Arbitration Solution

A platform can decide to change its arbitration solution at any time. For example, it can decide to switch from platform-managed dispute resolution to Kleros.

When changing arbitration strategy, the existing confirmed services will still be managed with the old arbitration solution.

### Updating Arbitration Fee Timeout

When a party requests to raise a dispute, the other party has a period of time to accept the dispute and proceed with its creation by paying the arbitration fee. If the time period expires, the dispute will be resolved in favor of the party who requested its creation.

A platform can customize the time period that a party has to accept a dispute.



