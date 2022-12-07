# TalentLayerID Recovery

Account recovery allows associating a [TalentLayerID](./) with another wallet of the same owner.

{% hint style="info" %}
**Good To Know:** Platforms can optionally implement recovery flows for their users. These flows are not required as core functionality for TalentLayer.
{% endhint %}

## Initiate a Recovery

In order to initiate a TalentLayerID recovery, you will need to have three things:

1. A TalentLayerID handle
2. The current wallet address.
3. The Recovery Password provided during TalentLayerID creation.

If you do not have access to your Recovery Password, there is unfortunately not any other way to recover your TalentLayerID.

## Verification of Wallet Ownership with Proof of Humanity

Proof of Humanity is a web-of-trust system that uses reverse Turing tests and dispute resolution to create a sybil-proof list of humans. TalentLayer users can optionally associate their TalentLayer IDs with their identity on Proof of Humanity during the TalentLayer ID creation process.

Proof of Humanity allows users to associate their human identity with one or more crypto wallets. Proof of Humanity can be used to prove that different wallets are associated with the same human and achieve things like emergency recovery of soul-bound tokens.

Currently, only members who verify their human-hood with Proof of Humanity are able to participate in emergency ID recovery. This is to prevent the recovery system from being used by bad actors to transfer their TalentLayer ID to another person’s wallet.

In the future, we hope to allow the association of various other sorts of IDs, ranging from KYC to anonymous sybil-resistant identities. These other associations may be used to recover TalentLayer IDs in the future.

## How Does it Work?

If a person loses access to their wallet (losing their private keys) holding their TalentLayer ID, TalentLayer uses Proof of Humanity to prove that the human behind the TalentLayer ID is requesting a recovery. Proof of Humanity POH has a way for them to assign their POH human identity with a different wallet.

### Creating a TalentLayer ID and Associating a POH ID

When a user creates their TalentLayer ID and associates it with a POH ID, TalentLayer sends a request to the POH registry verifying the wallet the user is logged in with is registered to a POH human identity.

### Initiating a Recovery By Proving Wallet Ownership

When a user wants to do a recovery of their TalentLayer ID (sending their ID NFT to a new wallet), TalentLayer sends a request to the POH registry to check if the POH identity is associated now with a new wallet. If it is associated with a new wallet, then we allow the recovery to initiate, sending the TalentLayer ID to the new registered wallet. If it is not associated with a new wallet, then we can assume the recovery initiation is fraudulent.

{% hint style="info" %}
**Good to know:** Currently, TalentLayer ID recovery is only possible for users who associate a Proof of Humanity identity with their TalentLayer ID during account creation.
{% endhint %}
