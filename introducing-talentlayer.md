# ☘ Introducing TalentLayer

## Is TalentLayer A Good Fit For Your Platform? <a href="#is-talentlayer-a-good-fit-for-your-platform" id="is-talentlayer-a-good-fit-for-your-platform"></a>

Are you looking to build platform like freelance marketplaces, bounty platforms, hackathon platforms, gig marketplaces, or something similar? TalentLayer is composable, decentralized, open-source infrastructure for labor markets; allowing anyone to easily build interoperable gig marketplaces. It is designed to empower workers to own their own reputation and access jobs without limitation. TalentLayer is optimized for a broad range of two-sided “labor platforms”, software platforms where users can complete services in exchange for payment. These platforms usually have a few things in common:

1. Hirers post tasks or other service engagements to the platform
2. Users complete work in exchange for payment
3. By completing work on the platform, users can build a reputation

TalentLayer offers a variety of tools to help labor platforms empower their users.

## Understanding TalentLayer Core's Components <a href="#understanding-talentlayer-cores-components" id="understanding-talentlayer-cores-components"></a>

TalentLayer Core is composed of the following key modules:

* ​[TalentLayer Universal Work Reputation Module ](https://docs.talentlayer.org/work-reputation-module)\[live 07/24/2022]
  * ​[TalentLayer ID System](https://docs.talentlayer.org/work-reputation-module/what-is-talentlayer-id)​
  * ​[TalentLayer Review System](https://docs.talentlayer.org/work-reputation-module/reviews-and-reputation)​
* ​[TalentLayer Universal Work Facilitation Module](https://docs.talentlayer.org/work-facilitation-module) \[live 10/18/2022]
  * ​[TalentLayer Universal Job & Proposal System](https://docs.talentlayer.org/work-facilitation-module/jobs-and-proposals)​
  * ​[TalentLayer Escrow & Dispute System](https://docs.talentlayer.org/work-facilitation-module/escrow-and-dispute-system)​

TalentLayer creates a paradigm shift in how freelance marketplaces operate by creating a universal reputation system and jobs repository that any marketplace can tap into. Users maintain one self-owned reputation across many marketplaces. Marketplaces that build on TalentLayer receive rewards by onboarding talent and jobs.

## How To Get Started Integrating TalentLayer Core into Your Platform <a href="#how-to-get-started-integrating-talentlayer-core-into-your-platform" id="how-to-get-started-integrating-talentlayer-core-into-your-platform"></a>

TalentLayer’s Alpha is currently live on a few chains and testnets. We are actively improving the protocol on a weekly basis and are working closely with integrating platforms to implement their feedback.

### Set Up Your Local Dev Environment <a href="#set-up-your-local-dev-environment" id="set-up-your-local-dev-environment"></a>

​[Local Environment Setup](https://docs.talentlayer.org/developers/local-environment-setup)​

### Explore The Indie Demo DAPP <a href="#explore-the-indie-demo-dapp" id="explore-the-indie-demo-dapp"></a>

Indie is an open-source fork-able codebase that is available for marketplaces and other platforms integrating with [TalentLayer](https://docs.talentlayer.org/) to borrow from and use to get inspired.Indie lays the groundwork for what will eventually become the TalentLayer SDK.View the TalentLayer Indie frontend on Github here:

{% embed url="https://github.com/TalentLayer-Labs/indie-frontend" %}

## We're Here to Help <a href="#were-here-to-help" id="were-here-to-help"></a>

Since TalentLayer Core is currently in **Alpha,** we recommend reaching out to the team on Twitter @TalentLayer before integrating directly with TalentLayer’s interoperable reputation and jobs systems.We are happy to help you:

1. 1.Understand how to implement TalentLayer on your platform: Every platform is a little different, and we want to know how we can best make our tech stack as composable as possible. By helping you, we learn too!
2. 2.Deploy TalentLayer on your platform’s native EVM chain: TalentLayer aims to be a cross-chain platform, and are in the process of spinning up implementations of our Alpha release on multiple EVM chains.

[Network Support](https://docs.talentlayer.org/developers/network-support)****

### Reading and Writing to TalentLayer Core <a href="#reading-and-writing-to-talentlayer-core" id="reading-and-writing-to-talentlayer-core"></a>

TalentLayer is multi-chain; that means there are implementations of TalentLayer Core living on multiple blockchains. Each platform must choose one TalentLayer Core chain implementation to write information to, and at least one TalentLayer Core chain implementation to read from.Writing is facilitated by connecting your platform with the various [TalentLayer Core smart contracts](https://docs.talentlayer.org/developers/smart-contracts) and triggering different actions.Reading is facilitated by searching data via the [TalentLayer Graph](https://docs.talentlayer.org/developers/graph-schema).For example, if you are running a freelancing marketplace and choose to host your Reputation and Jobs system on Polygon, you must integrate with the TalentLayer Core smart contracts on Polygon. Many of your users will have TalentLayer IDs on other chains as well as Polygon. To read reputation information from other chains, you can reference the TalentLayer Graphs on Polygon, Gnosis, and Ethereum to display holistic reputation data on your user interfaces.We are currently working on an SDK and better documentation to help platforms integrate more quickly. If you have any questions on interfacing with our smart contracts, reach out to us on [Twitter @TalentLayer](https://twitter.com/TalentLayer).

## Writing to TalentLayer Core <a href="#writing-to-talentlayer-core" id="writing-to-talentlayer-core"></a>

Writing is necessary to create a user’s TalentLayer ID, mint reputation updates, and create jobs.To write to TalentLayer Core, you must connect with the appropriate [TalentLayer smart contract](technical-guides/smart-contracts/) for the action you intend to take.

## Reading from TalentLayer Core <a href="#reading-from-talentlayer-core" id="reading-from-talentlayer-core"></a>

Reading is necessary to display repetitional and job information on your UI. You can create features such as:

* Reputation search pages
* Job search pages
* Pages that show a user their own reputation
* More

There are three key **data entities** that can be searched in the TalentLayer Graph:

1. 1.Job - A job that has been minted and it’s status
2. 2.User - A user’s TalentLayer ID NFT
3. 3.Review - A review that has been minted and associated with someone’s TalentLayer ID

The TalentLayer Graph is highly flexible: you can query and sort many diverse data points on jobs, reputations, identities, and how they associate with one another.

## Explore The Docs! <a href="#explore-the-docs" id="explore-the-docs"></a>

We’re working hard to document our tech stack. You can view our docs on our website below.Please stay tuned for updates and don’t hesitate to reach out with questions.[🌐What is TalentLayer Core?](https://docs.talentlayer.org/)

## TalentLayer’s Future Token Economics <a href="#talentlayers-future-token-economics" id="talentlayers-future-token-economics"></a>

As a decentralized protocol, TalentLayer will have an ecosystem token, incentives system, and fees system. These systems are not present in our Alpha. We expect to implement a V1 of our incentives and fees systems over the course of Winter 2022/2023. Please see our Economic Model Summary to better understand our thinking around tokenomics and fees. All information provided in the document below is not final - we will be working closely with integration partners to ensure fees and incentives align with their needs.​[TalentLayer Economic Model Summary \[NOT FINAL\]](https://www.notion.so/TalentLayer-Economic-Model-Summary-NOT-FINAL-fd99e6e616ca4f3c8dad191ab14aafe3)
