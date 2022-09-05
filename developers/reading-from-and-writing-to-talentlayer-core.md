# Reading From and Writing to TalentLayer Core

TalentLayer is multi-chain; that means there are implementations of TalentLayer Core living on multiple blockchains. Each platform must choose one TalentLayer Core chain implementation to write information to, and at least one TalentLayer Core chain implementation to read from. Please view [supported blockchains here](network-support.md).

Writing is facilitated by connecting your platform with the various [TalentLayer Core smart contracts](smart-contracts/) and triggering different actions.

Reading is facilitated by searching data via the [TalentLayer Graph](graph-schema.md).

For example, if you are running a freelancing marketplace and choose to host your Reputation and Jobs system on Polygon, you must integrate with the TalentLayer Core smart contracts on Polygon. Many of your users will have TalentLayer IDs on other chains as well as Polygon. To read reputation information from other chains, you can reference the TalentLayer Graphs on Polygon, Gnosis, and Ethereum to display holistic reputation data on your user interfaces.

### Writing to TalentLayer Core

Writing is necessary to create a user’s TalentLayer ID, mint reputation updates, and create jobs.

To write to TalentLayer Core, you must connect with the appropriate TalentLayer smart contract for the action you intend to take.

See [deployments here](deployments.md).

We currently have a fork-able codebase that is set up to interact with TalentLayer’s smart contracts: the Indie DAPP. That codebase can be found [here](https://github.com/TalentLayer/talentlayer-id-dapp).

We are currently working on an SDK and better documentation to help platforms integrate more quickly. If you have any questions on interfacing with our smart contracts, reach out to us on [Twitter @TalentLayer](https://twitter.com/TalentLayer).

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

[Explore the Graph here.](graph-schema.md)
