---
description: Basic understanding of the user identity on TalentLayer.
---

# TalentLayerID

{% hint style="info" %}
In Native Integrations, each user of a platform will have a TalentLayer ID. In On-Demand Integrations manage one master TalentLayerID that engages with the protocol on behalf of the platform's users. Learn more in the Options for Integration section of the documentation.&#x20;
{% endhint %}

## What is a TalentLayerID?

TalentLayer ID is a decentralized identity that allows ownership and growth of reputation across many service marketplaces. TalentLayer IDs are ERC-721 NFTs that live inside crypto wallets; this means that reputation is self-custodied by the wallet owner and lives separately from integrated platforms. TalentLayer IDs are “soul-bound” in that they can not leave the originating wallet after they have been used in a service engagement.

TalentLayerID is the core identity element for service buyers and sellers when interacting with TalentLayer-integrated marketplaces and freelancing tools. The TalentLayer ID is associated with reviews and represents the overall reputation in the ecosystem.

More information on how it is implemented can be found in out guide on the [TalentLayerID smart contract](../../technical-guides/lower-level-guides/smart-contracts/talentlayerid.sol.md).

## Role-Agnostic IDs

There is no concept of "separate accounts" for buyers and sellers.&#x20;

## TalentLayer ID Handles

Your TalentLayer ID Handle is a unique string of characters and numbers that you can choose when you create your TalentLayer ID. This handle is how others can search for your reputation.

You can have a maximum of 31 characters in your TalentLayer ID and use only low characters, numbers and - or \_.

{% hint style="info" %}
**Choose wisely:** Make sure you choose your handle carefully - after your ID has been initiated, your handle can not be changed.
{% endhint %}

## How to Get a TalentLayer ID

TalentLayer IDs can be minted on any platform integrated with TalentLayer during the user onboarding flow. They can also be claimed from TalentLayer directly on the following web page.

{% embed url="https://claim.talentlayer.org" %}

### How much do TalentLayer IDs cost

| CHARACTERS | PRICE (MATIC) |
| ---------- | ------------- |
| 5+         | 1             |
| 4          | 25            |
| 3          | 50            |
| 2          | 100           |
| 1          | 200           |

Standard TalentLayer IDs are between 5 and 31 characters long - they are available for minting for a symbolic 1 MATIC by anyone.\
\
Specialty TalentLayer IDs are between 1 and 4 characters long - these are available for purchase at the price rates below. Proceeds from TalentLayer ID sales go to fund TalentLayer’s open-source development.

### Can I trade TalentLayer IDs?

TalentLayer ID’s are Activity Bound NFTs - they are transferable until they are used to make any activity on TalentLayer. Activities include creating a job post, submitting a proposal, and other actions. Once a TalentLayer ID becomes active, they become soul-bound and can not be transferred.

## Learn More About The Tech

Learn more about the technical side of the TalentLayer ID in our Technical Guide on the smart contract.&#x20;

{% content-ref url="../../technical-guides/lower-level-guides/smart-contracts/talentlayerid.sol.md" %}
[talentlayerid.sol.md](../../technical-guides/lower-level-guides/smart-contracts/talentlayerid.sol.md)
{% endcontent-ref %}
