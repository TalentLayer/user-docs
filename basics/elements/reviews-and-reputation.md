# Reviews

****[**TalentLayerReview.sol**](https://github.com/TalentLayer/talentlayer-id-contracts) is the smart contract that handles reviews written to users' TalentLayer IDs. Reviews are minted as NFTs.

It can be broken up used to:

* Initiate of a review for a user, listing a counter-party to invite
* Mint a review to a user
* Look up reviews

TalentLayer ID’s build their reputation over time through receiving Reviews from counter-parties; people you’ve worked with either as a hirer or a person being hired.

A Review is an ERC 721 soulbound NFT that is associated with a TalentLayer ID. New Reputation NFTs are minted whenever a service is completed on TalentLayer. They include information about the service completed and a review from the other party. A TalentLayer ID can have an unlimited number of Reputation NFTs. Hirers leave Reputation NFTs for freelancers and freelancers leave Reputation NFTs for hirers - a mutual-review system.

## **Reviews During Account Recovery**

All review NFTs will follow the TalentLayer ID to the new wallet if an emergency account recovery is initiated.

{% hint style="info" %}
**Good to know:** Right now, there is no way to remove a review after it has been written. TalentLayer is working on a method for reviews that both parties agree should be removed to be deleted.
{% endhint %}
