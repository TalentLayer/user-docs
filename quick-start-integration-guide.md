# 🌿 Quick-Start Integration Guide

## Is TalentLayer A Good Fit For Your Platform?

Do you have an existing platform such as a freelance marketplace, bounty platform, hackathon platform, or something similar? Are you looking to build one of these platforms?

TalentLayer is composable, decentralized, open-source infrastructure for talent markets; allowing anyone to easily build interoperable gig marketplaces. It is designed to empower workers to own their own reputation and access jobs without limitation.

TalentLayer is optimized for a broad range of two-sided “labor platforms”, software platforms where users can complete services in exchange for payment. These platforms usually have a few things in common:

1. Hirers post tasks or other service engagements to the platform
2. Users complete work in exchange for payment
3. By completing work on the platform, users can build a reputation

TalentLayer offers a variety of tools to help labor platforms empower their users.

## Understanding TalentLayer Core's Components

TalentLayer Core is composed of the following key modules:

* [TalentLayer Universal Work Reputation Module ](broken-reference)\[live 07/24/2022]
  * [TalentLayer ID System](work-reputation-module/what-is-talentlayer-id.md)
  * [TalentLayer Review System](work-reputation-module/reviews-and-reputation.md)
* [TalentLayer Universal Work Facilitation Module](broken-reference) \[live 10/18/2022]
  * [TalentLayer Universal Job & Proposal System](work-facilitation-module/jobs-and-proposals.md)
  * [TalentLayer Escrow & Dispute System](work-facilitation-module/escrow-and-dispute-system.md)

TalentLayer creates a paradigm shift in how freelance marketplaces operate by creating a universal reputation system and jobs repository that any marketplace can tap into. Users maintain one self-owned reputation across many marketplaces. Marketplaces that build on TalentLayer receive rewards by onboarding talent and jobs.

## How To Get Started Integrating TalentLayer Core into Your Platform

TalentLayer’s Alpha is currently live on a few chains and testnets. We are actively improving the protocol on a weekly basis and are working closely with integrating platforms to implement their feedback.&#x20;

### We're Here to Help

Since TalentLayer Core is currently in **Alpha,** we recommend reaching out to the team on Twitter @TalentLayer before integrating directly with TalentLayer’s interoperable reputation and jobs systems.

We are happy to help you:

1. Understand how to implement TalentLayer on your platform: Every platform is a little different, and we want to know how we can best make our tech stack as composable as possible. By helping you, we learn too!
2. Deploy TalentLayer on your platform’s native EVM chain: TalentLayer aims to be a cross-chain platform, and are in the process of spinning up implementations of our Alpha release on multiple EVM chains.

{% content-ref url="developers/network-support.md" %}
[network-support.md](developers/network-support.md)
{% endcontent-ref %}

{% hint style="danger" %}
**Impending Metadata Update:** Please be aware of our **metadata update** that took place in October 2022. To guarantee that your implementation will interface with the TalentLayer interoperable jobs repository and/or reputation system you must update your system to the V3 of our data model. The existing data schema does not include a key identifier that represents originating marketplaces/platforms - something necessary for the TalentLayer contracts to know the difference between the various actors writing data to TalentLayer. All future data schema updates should not impact interoperability. We appreciate your flexibility as we move closer to this update!
{% endhint %}

## Reading and Writing to TalentLayer Core

TalentLayer is multi-chain; that means there are implementations of TalentLayer Core living on multiple blockchains. Each platform must choose one TalentLayer Core chain implementation to write information to, and at least one TalentLayer Core chain implementation to read from.

Writing is facilitated by connecting your platform with the various [TalentLayer Core smart contracts](developers/smart-contracts/) and triggering different actions.

Reading is facilitated by searching data via the [TalentLayer Graph](developers/graph-schema.md).

For example, if you are running a freelancing marketplace and choose to host your Reputation and Jobs system on Polygon, you must integrate with the TalentLayer Core smart contracts on Polygon. Many of your users will have TalentLayer IDs on other chains as well as Polygon. To read reputation information from other chains, you can reference the TalentLayer Graphs on Polygon, Gnosis, and Ethereum to display holistic reputation data on your user interfaces.

### Fork-able Frontend Codebase

We currently have a fork-able codebase that is set up to interact with TalentLayer’s smart contracts: the Indie DAPP. That codebase can be found here:

{% content-ref url="what-is-indie.md" %}
[what-is-indie.md](what-is-indie.md)
{% endcontent-ref %}

We are currently working on an SDK and better documentation to help platforms integrate more quickly. If you have any questions on interfacing with our smart contracts, reach out to us on [Twitter @TalentLayer](https://twitter.com/TalentLayer).

### Writing to TalentLayer Core

Writing is necessary to create a user’s TalentLayer ID, mint reputation updates, and create jobs.

To write to TalentLayer Core, you must connect with the appropriate TalentLayer smart contract for the action you intend to take.

{% content-ref url="developers/deployments.md" %}
[deployments.md](developers/deployments.md)
{% endcontent-ref %}

### Reading from TalentLayer Core

Reading is necessary to display repetitional and job information on your UI. You can create features such as:

* Reputation search pages
* Job search pages
* Pages that show a user their own reputation
* More

There are three key **data entities** that can be searched in the TalentLayer Graph:

1. Job - A job that has been minted and it’s status
2. User - A user’s TalentLayer ID NFT
3. Review - A review that has been minted and associated with someone’s TalentLayer ID

The TalentLayer Graph is highly flexible: you can query and sort many diverse data points on jobs, reputations, identities, and how they associate with one another.

## Explore The Docs!

We’re working hard to document our tech stack. You can view our docs on our website below.

Please stay tuned for updates and don’t hesitate to reach out with questions.

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

## TalentLayer’s Future Token Economics

As a decentralized protocol, TalentLayer will have an ecosystem token, incentives system, and fees system. These systems are not present in our Alpha. We expect to implement a V1 of our incentives and fees systems over the course of Winter 2022. Please see our Economic Model Summary to better understand our thinking around tokenomics and fees. All information provided in the document below is not final - we will be working closely with integration partners to ensure fees and incentives align with their needs.&#x20;

[TalentLayer Economic Model Summary \[NOT FINAL\]](https://www.notion.so/TalentLayer-Economic-Model-Summary-NOT-FINAL-fd99e6e616ca4f3c8dad191ab14aafe3)
