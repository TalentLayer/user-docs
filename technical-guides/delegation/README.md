# Delegation

## Intro to Delegation

Delegation enables platforms to take actions and cover costs of users interacting with their UI. This is possible thanks to meta-transactions - a standard way for a third-parties to send another user’s transactions on the original user's behalf.&#x20;

## Use Case of Delegation

The goal of the delegation system is to allow users to give the right to third party accounts (called **delegates**) to perform actions on the protocol on their behalf.

The main use cases can be:

* **covering user fees**: platforms can perform actions on behalf of the users, covering their fees
* **account abstraction:** platforms can abstract away the complexity of having to approve transactions for their users by taking those actions for them
* **plugins**: users can delegate actions to plugins for automation, scheduling, smoother experience, etc..

This system can also achieve a much better UX for users. Once they have a TalentLayer ID, they only need to call one function to link a new delegate to their profile.

The delegate can now call functions for the user, who won’t have to send transactions or sign messages anymore.

## Limits of Delegation

Delegates will only be able to perform actions that don’t touch user funds. Operations that involve user funds will have to be done directly by the user, both for security and technical reasons.

These operations are:

* accept proposal making a deposit in the escrow
* pay arbitration fee to raise dispute

The delegates are linked to a profile, so this means that they cannot be used to mint a TalentLayer id for a user.

## TalentLayer's Implementation

We have implemented a delegation system in contracts that the user interacts with:

* TalentLayerID
* ServiceRegistry
* TalentLayerEscrow
* TalentLayerReview

To support this, we've enabled:

* tracking the list of delegates for each TalentLayer ID
  * this state will be stored in `TalentLayerID` and the other contracts will read from it
* allowing users to add and remove a delegate
* for each function that supports delegation: enabling checking whether the user is either the owner or a delegate of the involved profile
