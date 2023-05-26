# Introduction

## An Intro to TalentLayer’s Architecture

Hey, everyone! We talk a lot about the high-level vision for TalentLayer, but now it’s time for our first technical deep dive blog post. Glad to have you along for the ride.

In this post we aim to help you…

* Gain a better understanding of the design principles behind TalentLayer’s architecture
* Understand the various main technical components of TalentLayer
* Understand how features that TalentLayer enables can complement your platform’s current offerings

## D**esign principles behind TalentLayer’s architecture**

We'll begin this memo by discussing the decisions we made regarding security, scalability, and decentralization.

#### Philosophical Principles

When building our technology stack, we followed some philosophical design principles at the protocol level (think of TalentLayer level) to help guide our decisions. Here is a list of these design principles.

⭐ **Keep It Stupid Simple:** We keep our protocol and smart contracts as simple as possible.

⭐ **FrictionLess:** We remove any friction in the protocol to make the platform and end users’ experience as easy as possible.

**⭐ Optimistic:** We \*\*\*\*assume by default that the user and platforms will act in goodwill for the good of the ecosystem.

⭐ **Autonomous protocol:** We create incentives for the ecosystem to act for the good of the platform and prevent bad behaviors. We incentivize good quality and good behavior.

⭐ **Platform Compliance:** Platforms \*\*\*\*have to be compliant with the rules. Thus we facilitate the spirit of fairness and support within the network and create new on-chain information that anyone can use upon their wish.

⭐ **User Sovereignty:** Users have ownership of all the content they create: service, proposal, and all the reviews they receive. Although on a platform level we allow some restrictions against a user, we aim to always give the user alternative somewhere else in the protocol (e.g. another platform).

⭐ **Reputation is everywhere:** Having an open system is all about reputation, everything is public, and every action of a user or a platform in the protocol can be used as a tool to calculate a new form of reputation. We remain open-minded that reputation can mean different things to different people and we let the marketplaces do their own interpretation.

#### Un-censorable, User-Owned Data

We believe that the user (worker) is the owner of the content they create on our platform. Here's an example to illustrate our belief:

Let's say a user creates a service (service is equal to job in the context of TalentLayer) for a developer search. They become the owner of the job post and the content associated with it. The user then posts the service on a platform (think of job marketplace), which becomes associated with this service. If everything goes well, the platform is rewarded for helping the user to post and to manage the service. However, if there's a problem with the service - say, a platform realizes that it’s been posted by a person in a jurisdiction they don’t serve, the platform has the right to remove the association with the service post and the content creator, and it won't receive any money from this service. When the association with the service is discontinued the link with the service will be removed on-chain. The service will be still there with the user but it won’t be visible on the originating job marketplace.

We don't want users to be removed from the protocol, so we enable marketplaces to individually remove them at the platform level. In this scenario, the user would be able to access other platforms that do want to serve them; all while maintianing their reputation, job posts, and data. This allows platforms to uphold any legal responsibilities they have based on their jurisdiction or policies, while still allowing users full data custody.

These design principles define decisions made on the smart contact level. TalentLayer operates at the protocol level, which means we face similar challenges, but on a different scale. We’re as decentralized, secure and scalable as the components in our architecture are.

#### Scalability

Initially, we made a conscious decision to be more centralized, but we plan to slowly transfer the governance of our smart contracts to a DAO over time. This is necessary in order to make TalentLayer something that lives on for many decades, regardless of the TalentLayer Core Team.

When it comes to scalability, we are taking steps to ensure that our smart contracts are able to manage millions of jobs and services in the future. While we initially optimize for quick entry into the market, we are aware that improvements will be necessary as we move forward.

When it comes to security, our main focus is on creating mechanisms to prevent and reduce any malicious activity within TalentLayer. Although we've made some concessions to enter the market quickly, we're confident in our ability to prevent any negative usage. We strive to keep our smart contracts simple and have multiple layers of security in place, including at the smart contract level, indexer level, and frontend level. We've made our smart contracts upgradable in key areas to allow for improvements over time; these upgradable elements are currently managed by the TalentLayer Core team and will be handed to a DAO once TalentLayer’s governance decentralizes. It’s worth noting that no upgradable mechanisms impact flow of funds in escrow.

## Overview of TalentLayer architecture

Here is a simple illustration of TalentLayer tech stack and data flow.

<figure><img src="../.gitbook/assets/Untitled.png" alt=""><figcaption></figcaption></figure>

Let’s unpack now all different layers we have at TalentLayer architecture.

On the bottom, as a foundational layer, we have the **Blockchain layer**. There we will have different blockchains but at the time of writing this memo our main focus is [Polygon](https://polygon.technology/developers).

Then on top of this blockchain layer, we’ve got the so called **Application Layer**. This is where the TalentLayer protocol sits. Our protocol is made of **Smart Contracts**. These smart contracts we split in different modules, e.g. Identity module, Platform module, Service, module, Escrow module, Dispute Resolution module and Review module.

On top of the Application layer we have the **Indexer layer**. This layer is empowered by [TheGraph](https://thegraph.com/docs/en/). The purpose of this layer is to get all the data from the blockchain and make it easily readable by anyone who builds or participates in a marketplace.

At the very top of our tech stack we have the different kinds of **Marketplaces** that communicate directly with the Indexer layer and leverage our tech stack (TalentLayer protocol).

These marketplaces have basically two types of interaction with the protocol.

*   The first, let’s call it the easy one, is READING data. This is when marketplaces get information stored in the protocol, like getting all the open services. They’re getting that data by connecting with the **Indexer layer** via an API (see this example👇 where you can get data from the protocol by querying the graphQL API )

    [https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol](https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol)).
* The second operation that marketplaces can perform is WRITING data (think of storing data). When they write data they are calling directly TalentLayer smart contracts. Effectively they are adding data to the blockchain. By “calling”, we mean here sending a transaction request to the blockchain. In this request we detail, which contract we want to use, which function and with which parameters. (e.g.: the TalentLayer ID smart contract, the mint function, with the parameters “Mitko”)

## Blockchain (Foundation) Layer

TalentLayer protocol and all the things we are building sit on on top of the blockchain. We chose to build on blockchains on Layer 2, because it doesn’t make sense for us to build on top of Layer 1. L1s, like [Ethereum](https://ethereum.org/en/), have got expensive gas fees. In addition, it is not optimal for users to interact with the protocol at this level (it creates a lot of complexity and work if we build our components on top of L1).

When deciding whether to be or not to be blockchain agnostic there were two main rationales, and related trade offs, that we considered:

* Business rationale - we believe it is better to be on different chains and attract different kinds of marketplaces and communities. This would help us creating network effects, build liquidity pool of talent and keep our options as broad as possible.
* Technical rationale - from a technical point of view it is much easier to build and be only on one chain. It is easier because at the moment it is hard for the blockchains to communicate between each other. If a user creates his own NFT identity on [Polygon](https://polygon.technology/developers), let’s call it “Mitko”, someone else can create an NFT with identity “Mitko” on Avalanche. The original NFT creator have no way of checking that.

Essentially, we face competing incentives from business and technical point of view and we needed to make a trade off. We are committed to be blockchain agnostic but at the time of writing this memo we are fully focus on building on [Polygon](https://polygon.technology/developers).

We won’t try to solve the problem of cross chain interaction. In case some other project figures out the problem of cross chain interaction we will leverage this in the future.

One solution we don’t currently have is the technical solution for the problem with unique identities on marketplaces built on different blockchains. This is another reason why protocols like [Lens](https://www.lens.xyz/) stay only on one blockchain ([Polygon](https://polygon.technology/) in their case).

Our approach is more aligned with the technical rationale at this stage. We remain however customer focused and the choice of which blockchain to build on in the future will be driven by our customers’ needs. If the customer wants to build on Avalanche, we will make this work. If the customer chooses another blockchain to build on, again we’ll make it work.

### How do we interact with blockchain?

To interact with the blockchain we use the [RPC Endpoint](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/). When someone wants to communicate and to ask something the blockchain then the [RPC Endpoints](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) are taking care of sharing this with the blockchain nodes. TalentLayer as a protocol don’t have to communicate directly with the blockchain (nodes). [RPC Endpoints](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) are doing this for us.

## Smart contracts layer

### Overview

At the core of TalentLayer protocol are six smart contracts. Our engineering team has written all these six smart contracts. Here they are for the TestNet:

[https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/.deployment/mumbai.json](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/.deployment/mumbai.json)

<figure><img src="../.gitbook/assets/Untitled 1.png" alt=""><figcaption></figcaption></figure>

1. [TalentLayer ID smart contract](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerID.sol) (+screenshot and the address) where we handle user identity.
2. [TalentLayer Platform ID contract](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerPlatformID.sol) (+screenshot and the address) where we handle the identity of platforms.
3. [TalentLayer Service Registry smart contract](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerService.sol) when we have all the logic and workflow of creating a service and proposal.
4. [TalentLayer Escrow smart contract](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerEscrow.sol) is the most complex of our contracts because it handles the money part. This is where we face the most complexity and spend most time on development. It is link closely with TL arbitrator contract.
5. [TalentLayer Review smart contract](https://github.com/TalentLayer/talentlayer-id-contracts) that handles all the logic around the reputation and the rating.
6. [TalentLayer Arbitrator smart contract](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerArbitrator.sol) - handles conflict and dispute resolution matters.

For some smart contracts we use established standards (NFT, dispute resolution) as this allows us to be more secure and have more interoperable features.

We decided to have all of our 6 smart contracts upgradeable because we are a young project and we understand that we will continue to iterate and improve them. We retain the power to change the contracts but we also need to gain the trust of our customers that we will use this power for the good of the protocol. In the future, we want to ensure that the protocol can go and live alone on its own governed by its community.

### How do we feel about someone forking our smart contracts?

For us it is ok if someone wants to fork us. We think that the value of using us is to have different pools of liquidity and different platforms implementing us and sharing this liquidity. We decided to keep our smart contracts open source and anyone can fork us. But they would need to start from scratch to build the liquidity of talent. It is not an easy task and this can split the liquidity (as it happened with Uniswap when it got forked). We are ready to take this risk.

### Deep Dive

Let’s unpack now how users and marketplaces interact with the blockchain. This all happens on smart contract level. Smart contracts are at the core of TalentLayer protocol. This is where the magic happens! This is what makes TalentLayer unique.

Whenever someone calls the protocol they actually let the users in her marketplace interact with different smart contracts. Every time anyone writes they actually interact with the protocol via a transaction that contacts one of the six smart contract modules.

Let’s take the Identity module as an example (it is called [TalentLayerID](https://docs.talentlayer.org/technical-guides/smart-contracts/talentlayerid.sol)). If Alice wants to create an identity she has to call a function within this contract and at the end of the transaction there will be new data written on the blockchain (added to the Blockchain Layer of our tech stack). Each of our contracts are and will be deployed on each of the chains we build on (at the moment they are deployed on [Polygon](https://polygon.technology/developers)). This means that we will have an address with a code linked to that address stored somewhere on the chain so the marketplace will have an amount of disc space to write on. It is alike a small database. Every smart contract has this small database and an address linked to that and the code linked to this address. So in a nutshell, we have our smart contracts written for the blockchain/s that we have marketplaces built on. Whenever a data is written on on a dedicated database on the blockchain it is written using this smart contract.

The service that we use to write this data on the chain, which is a common way to write on chain, is called [RPC endpoint API](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/). RPCs are servers that let apps read from and submit transactions to blockchains. In the illustration of our architecture we call these **RPC CALL**.

How does this RCP CALL work?

When Alice wants to write on a certain chain, she makes an http request. The [RPC API](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) is responsible to send (communicate) this request to the chain (Polygon in our case). This will be a new request and it is executed by a node running the chain. For the [RPC endpoint](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) we’re not running our own node but we use a service provider.

Users are interacting via their wallets and Ethereum address when signing a transaction and proving that they are they. For example if the call that Alice makes comes from [Metamask](https://metamask.io/) wallet, under the hood we use a node that services [Metamask](https://metamask.io/). Whenever Alice authenticates using her [Metamask](https://metamask.io/) wallet, we automatically allow the node that [Metamask](https://metamask.io/) is using to run the [RPC endpoint](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) to actually write this data on the blockchain. A marketplace can use any type of [RPC endpoint](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) (typically there are several endpoints for one chain). It is up to marketplace to decide. We remain flexible and do not impose any restrictions on that. The data that we normally use [RPC endpoints](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) to write data on the blockchain is very limited.

## IPFS Off-chain Data

It is important to note that storing data on chain is really expensive (much more expensive on storing it on Web 2 database). This is why we store the minimal amount of data needed to apply the logic of the smart contract. More specifically, for [TalentLayer Identity ID](https://docs.talentlayer.org/technical-guides/smart-contracts/talentlayerid.sol) we store on chain only the ID of the user, which is a numerical data such as 23. We also store a handle, in a string format, for example “Mitko”, to make sure that if one is minted it won’t be minted again. The only way to ensure that is to have this information stored on chain.

To store data off-chain we use [IPFS API ID (CID)](https://docs.ipfs.tech/concepts/content-addressing/). In our tech stack [IPFS](https://docs.ipfs.tech/) is key when it comes to storing data off-chain. In the smart contract we know that “Mitko” got his description, profile etc. in a particular [CID](https://docs.ipfs.tech/concepts/content-addressing/) stored on [IPFS](https://docs.ipfs.tech/). An [CID](https://docs.ipfs.tech/concepts/content-addressing/) on [IPFS](https://docs.ipfs.tech/) looks like a random text string key and we store that string ID also on chain. To fetch that data that is stored on chain in the future we use the Indexer layer.

## What Does Indexer Layer Do?

Indexer Layer makes it easier for marketplaces to get any kind of data (on and off chain). This layer does two main things.

* First, it listens everything that happens on the smart contract side (an event), and if an event happens that needs the data (or part of it) to be copied, it will do that. In other words it deals with anything related to writing data. Every time an action happens on the smart contract level we trigger an event. That means that someone listens for this and can do something with it (e.g. tell to the blockchain that something happened). For example, an event could be when someone creates a new identity, e.g. ID 23 with a handle “Mitko” and with a specific off chain ID. This becomes an event and the Indexer Layer is responsible for listening to that event and storing that on Web2 database (MySQL database). This way the data is very easy to be written.
* Second, the Indexer gives us an API ([TheGraph API](https://thegraph.com/docs/en/querying/graphql-api/) in our case) to read the data from the database that is already written there.

To protect the data privacy we use the [TheGraph](https://thegraph.com/docs/en/) protocol. [TheGraph](https://thegraph.com/docs/en/) basically leverages Web2 tech to store the data but still making it sure it is stored in a trustless way. This is done via a network of nodes that is responsible for reading the event and confirming that this is a real event.

The role of the Indexer is to check every transaction happening on the blockchain. This is the kind of information that the Indexer is reading. They are doing that only for the specific contract, i.e. reading that information using their own [RPC Endpoints](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/). Inside of that they can have a list of events. They use these events to index data. They are basically reading a transaction, which in a more abstract way is an object with a bunch of info in there (hash, status) and an array of events and this is the most important part that the Indexer will check too.



<figure><img src="../.gitbook/assets/Untitled 2.png" alt=""><figcaption></figcaption></figure>

## What happens under the hood?

Let’s illustrate end-to-end flow across the TalentLayer tech stack with an example:

1. A user creates an identity on Marketplace A, let’s say ID “23” and string “Mitko”
2. Marketplace A sends a transaction to the blockchain to the [TalentLayer ID module](https://docs.talentlayer.org/technical-guides/smart-contracts/talentlayerid.sol) (smart contract) executing the mint function of the [TalentLayer ID](https://docs.talentlayer.org/basics/readme/what-is-talentlayer-id#what-is-a-talentlayerid)
3. A request is sent to a blockchain to execute this transaction
4. This transaction is then sent to the blockchain linked to this smart contract, which means that we ask a node to run this function with ID “23” and “Mitko” parameters
5. The transaction gets executed, on a blockchain level
6. After 2-3 seconds the new transaction is accepted on the blockchain (e.g. on [Polygon](https://polygon.technology/developers)) and eventually it is added to a block
7. Once included to a block and executed then the frontend can check that the transaction is successful and if it is confirmed to present the result to the user
8. This allows the Indexer Layer to start reading directly on the chain to get the event using their own [RPC endpoint](https://moralis.io/ethereum-rpc-nodes-what-they-are-and-why-you-shouldnt-use-them/) (listen for events).
9. The Indexer ([TheGraph](https://thegraph.com/docs/en/)) then executes a function developed by TalentLayer called _handlemint_ (essentially we’re asking [TheGraph](https://thegraph.com/docs/en/) to execute this function every time it sees a new mint event).
10. When [TheGraph](https://thegraph.com/docs/en/) runs this function it executes part of the code that we wrote. This code is asking [TheGraph](https://thegraph.com/docs/en/) to create a new entity (user entity, an object) and in this user entity we execute the _handlemint_ function that takes some information from the event (e.g. ID handle) and saves that in [TheGraph](https://thegraph.com/docs/en/) database.
11. This concludes the first stage, i.e. getting the information about an event stored

There is another process, which runs in sync and is triggered by an off-chain event, related to the off-chain information that is also handled by [TheGraph](https://thegraph.com/docs/en/).

1. First [TheGraph](https://thegraph.com/docs/en/) calls an IPFS endpoint, similar to API, to get the off chain data (this is something that happens in sync and is triggered by an on-chain event)
2. The same way that we write a _handlemint_ function for the event we write a handle function to take care of this off chain data and to tell to [TheGraph](https://thegraph.com/docs/en/) to create a new entity (called User Description) and this sits in the database on the Indexer.
3. In this User Description entity we will copy all the information on [IPFS](https://docs.ipfs.tech/) (name, description, skills etc.)
4. Marketplace A will wait for [TheGraph](https://thegraph.com/docs/en/) to add this new user and when we detect that this user is added to [TheGraph](https://thegraph.com/docs/en/) we can show to the user a success message that the process is completed and you can start using the protocol. This process is basically whenever we mint a new user we send a data and on the front end we ask [TheGraph](https://thegraph.com/docs/en/) using their [API](https://thegraph.com/docs/en/querying/graphql-api/) about the data related to this new user. In the beginning when this data is not on [TheGraph](https://thegraph.com/docs/en/) it returns an empty response and then after 2-3 seconds we have the full response with all the user information which means this a success and the data is indexed.

To match the off chain and on chain data we first use the on chain data of the mint event (the one that is triggered when you create a profile). This is the most trustworthy information we’ve got. Inside that we will have a user ID which is the on chain data that is already stored with the handle chosen and the ID of the off chain IPFS data. As a flow this looks like:

1. We get an onChain event when a profile is created (minted). This event contains the following data: the ID of the user, his handle, and the CID of the IPFS off chain data
2. The indexer get this event, processes the information and then query IPFS CID to get extra information

What happens below the hood is that [TheGraph](https://thegraph.com/docs/en/) receives these events (receive the event meaning Indexer is checking every 10 sec for new transaction and extract the events). We call our function telling it that “I create a new user with the ID 23 and a handle “Mitko” and off-chain data with this [CID](https://docs.ipfs.tech/concepts/content-addressing/)” and then the off chain will be handled in a separate process. This way we are 100% sure that this data will never move because [IPFS](https://docs.ipfs.tech/) data is immutable, i.e. if you change the data that you store on [IPFS](https://docs.ipfs.tech/) it will change the identity. When you query the [IPFS](https://docs.ipfs.tech/) data you’ll get the data (description, skills etc.)

For now we write data directly on [IPFS](https://docs.ipfs.tech/) and we do not use other tools to make our data on [IPFS](https://docs.ipfs.tech/) perpetual (if data is not used over time it will be removed from [IPFS](https://docs.ipfs.tech/)).

We have the Indexer Layer that is taking care of the [IPFS](https://docs.ipfs.tech/) data where we have a cash version of all the data so in case we lose the [IPFS](https://docs.ipfs.tech/) (i.e. IPFS files, e.g. the file where you put a description) we don’t need it anymore as it is stored in [TheGraph](https://thegraph.com/docs/en/).

Reading into the [IPFS](https://docs.ipfs.tech/) is slow and painful. Therefore we have this data also added to [TheGraph](https://thegraph.com/docs/en/). In the first TalentLayer version the Indie was designed to allow the frontend to go and check the off-chain data from [IPFS](https://docs.ipfs.tech/) and this took so long that it made it impossible for the marketplace to query the data inside [IPFS](https://docs.ipfs.tech/). That is why we put efforts to improve [IPFS](https://docs.ipfs.tech/) and data integration. This data integration is on the Indexer Layer now and it allows the marketplace to fetch that data very quickly w/o relying on [IPFS](https://docs.ipfs.tech/).

Example of such query: [https://docs.talentlayer.org/technical-guides/graph-schema#filtering-services-based-on-different-attributes](https://docs.talentlayer.org/technical-guides/graph-schema#filtering-services-based-on-different-attributes))

This is a query where you can check all the information that is stored on [TheGraph](https://thegraph.com/docs/en/), on the official endpoint for TalentLayer listed here in our documentation: [https://docs.talentlayer.org/technical-guides/graph-schema#exploring-the-subgraph](https://docs.talentlayer.org/technical-guides/graph-schema#exploring-the-subgraph). This means that anyone can go and see what kind of data we’ve got. There is a an explorer schema where all the entities we’ve talked about can be seen that you can query.

For example, if you get to the user entity, it explains to you that you’ve got the ID, the handle and the CID (off-chain data identity), the description, the skills the country etc. Everything on [TheGraph](https://thegraph.com/docs/en/) is public and you can see all the data you can query.

Here is an example ([GraphQl API](https://thegraph.com/docs/en/querying/graphql-api/)) of a request for getting services

<figure><img src="../.gitbook/assets/Untitled 3.png" alt=""><figcaption></figcaption></figure>

You open the jobs and order them by the date they were created. You choose also the number of services you want and specify on which platform they were opened. You can see the ID of the service, when it was created, and what is the status, on which platform it was created, the freelancer, the hirer etc. + all the off chain information about the service.

At the end this is what the marketplace has to request with these kind of objects asking for the data they want.

All this data is public and anyone can see this data outside of [TalentLayer](https://docs.talentlayer.org/). You go to a public Url with a tool called [Hasura](https://cloud.hasura.io/public/graphiql?endpoint=https%3A%2F%2Fapi.thegraph.com%2Fsubgraphs%2Fname%2Ftalentlayer%2Ftalent-layer-protocol) using TalentLayer’s endpoint address.

<figure><img src="../.gitbook/assets/Untitled 4.png" alt=""><figcaption></figcaption></figure>

## How do we manage smart contracts?

Each contract has an owner and we use [OpenZeppelin Defender](https://www.openzeppelin.com/defender) to manage, automate and ship our smart contracts. We have a multi-sign system in place (multi-sign account by [Gnosis Safe](https://safe.global/)) where a few members of the core TalentLayer team decide and approve decisions related to upgrading the contracts.

## What development tools are we using?

We mostly use [VisualStudio](https://code.visualstudio.com/) to code and we use [Hardhat](https://hardhat.org/hardhat-vscode/docs/overview) for VisualStudio to manage and compile smart contracts.

For the frontend we are using React.js which is the most common one used in the space. We are using Typescript, we are using [Tailwind CSS](https://tailwindcss.com/docs/font-style) for the styling, and some libraries like [iterate.js](https://github.com/topics/iterate-js-library) to make it simple to communicate with RPC client. This way the builders can build marketplace very quickly.

We are using JavaScript to query the Indexer ([TheGraph](https://thegraph.com/docs/en/)). [TheGraph](https://thegraph.com/docs/en/) gives us an [API](https://thegraph.com/docs/en/querying/graphql-api/) so we can query and get all the data we need.

[Initial Questions](https://www.notion.so/Initial-Questions-07285bdf073a40fe9a8e8163f6bd12a6)
