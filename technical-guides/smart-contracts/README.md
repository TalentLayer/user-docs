---
description: >-
  In this guide we will take a close look at each smart contract's structure and
  function
---

# Smart Contracts

## Writing to TalentLayer Core

TalentLayer is multi-chain. Each platform must choose one TalentLayer Core chain implementation to write information to.

Writing is facilitated by connecting your platform with the various TalentLayer Core smart contracts and triggering different actions.

Writing is necessary to create a user’s TalentLayer ID, mint reputation updates, and create services.

To write to TalentLayer Core, you must connect with the appropriate TalentLayer smart contract for the action you intend to take.

We currently have a fork-able codebase that is set up to interact with TalentLayer’s smart contracts: the Indie DAPP. That codebase can be found [here](https://github.com/TalentLayer-Labs/indie-frontend).

## Permission to Write

As of today, only platforms may write to TalentLayer. In order to get registered as a platform, learn more about requesting a Platform ID here:

{% content-ref url="../../basics/elements/platformid.md" %}
[platformid.md](../../basics/elements/platformid.md)
{% endcontent-ref %}
