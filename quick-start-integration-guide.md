# 🌿 Quick-Start Integration Guide

## How To Get Started Integrating TalentLayer Core into Your Platform

TalentLayer’s Alpha is currently live on a few chains and testnets. We are actively improving the protocol on a weekly basis and are working closely with integrating platforms to implement their feedback.

### We're Here to Help

Since TalentLayer Core is currently in **Alpha,** we recommend reaching out to the team on Twitter @TalentLayer before integrating directly with TalentLayer’s interoperable reputation and services systems.

We are happy to help you:

1. Understand how to implement TalentLayer on your platform: Every platform is a little different, and we want to know how we can best make our tech stack as composable as possible. By helping you, we learn too!
2. Deploy TalentLayer on your platform’s native EVM chain: TalentLayer aims to be a cross-chain platform, and are in the process of spinning up implementations of our Alpha release on multiple EVM chains.

{% content-ref url="developers/network-support.md" %}
[network-support.md](developers/network-support.md)
{% endcontent-ref %}

{% hint style="danger" %}
**October Metadata Update:** Please be aware of our **metadata update** that took place in October 2022. To guarantee that your implementation will interface with the TalentLayer interoperable services repository and/or reputation system you must update your system to the V3 of our data model. The previous versions of our data schemas do not include a key identifier that represents originating marketplaces/platforms - something necessary for the TalentLayer contracts to know the difference between the various actors writing data to TalentLayer. All future data schema updates should not impact interoperability.
{% endhint %}

## Reading and Writing to TalentLayer Core

TalentLayer is multi-chain; that means there are implementations of TalentLayer Core living on multiple blockchains. Each platform must choose one TalentLayer Core chain implementation to write information to, and at least one TalentLayer Core chain implementation to read from.

Writing is facilitated by connecting your platform with the various [TalentLayer Core smart contracts](developers/smart-contracts/) and triggering different actions.

Reading is facilitated by searching data via the [TalentLayer Graph](developers/graph-schema.md).

For example, if you are running a freelancing marketplace and choose to host your Reputation and Services system on Polygon, you must integrate with the TalentLayer Core smart contracts on Polygon. Many of your users will have TalentLayer IDs on other chains as well as Polygon. To read reputation information from other chains, you can reference the TalentLayer Graphs on Polygon, Gnosis, and Ethereum to display holistic reputation data on your user interfaces.

### Fork-able Frontend Codebase

We currently have a fork-able codebase that is set up to interact with TalentLayer’s smart contracts: the Indie DAPP. That codebase can be found here:

{% embed url="https://github.com/TalentLayer/talentlayer-id-dapp" %}

We are currently working on an SDK and better documentation to help platforms integrate more quickly. If you have any questions on interfacing with our smart contracts, reach out to us on [Twitter @TalentLayer](https://twitter.com/TalentLayer).

### Writing to TalentLayer Core

Writing is necessary to create a user’s TalentLayer ID, mint reputation updates, and create services.

To write to TalentLayer Core, you must connect with the appropriate TalentLayer smart contract for the action you intend to take.

{% content-ref url="developers/deployments.md" %}
[deployments.md](developers/deployments.md)
{% endcontent-ref %}

### Reading from TalentLayer Core

Reading is necessary to display information about reputation and services on your UI. You can create features such as:

* Reputation search pages
* Service search pages
* Pages that show a user their own reputation
* More

There are three key **data entities** that can be searched in the TalentLayer Graph:

1. Service - A service that has been minted and it’s status
2. User - A user’s TalentLayer ID NFT
3. Review - A review that has been minted and associated with someone’s TalentLayer ID

The TalentLayer Graph is highly flexible: you can query and sort many diverse data points on services, reputations, identities, and how they associate with one another.

## Explore The Docs!

We’re working hard to document our tech stack. You can view our docs on our website below.

Please stay tuned for updates and don’t hesitate to reach out with questions.

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

