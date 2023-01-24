# Fees & Economics

## Escrow-Related Fees

Three types of fees are levied at the release of an escrow transaction (after a job has been completed, and if there were any disputes, they have been resolved).&#x20;

These fees enable TalentLayers' interoperability between multiple marketplaces; allowing marketplaces to make money on users and jobs they onboard to the protocol even if they do transactions on other platforms or with users of other platforms.

### Originating Platform Fee (2%)

This fee is a flat fee that is remitted to the originating platform of each user in the transaction. **An Originating Platform is defined as the platform that a user minted their TalentLayer ID through.** The fee proceeds are split 50%-50% between the Originating Platform of each user.&#x20;

Example 1: User A was onboarded by Platform G and User B was onboarded by Platform M. When these two users transact, each originating platform gets 50% of the Originating Platform Fee proceeds.&#x20;

Example 2: User A and User B were both onboarded by Platform G. Platform G receives 100% of the Originating Platform Fee from any transactions these users complete together (50% for originating User A and 50% for originating User B)

### Platform Fee (0%-100%)

This is a fee that is configured by platforms for jobs that are posted by that platform  on behalf of a user to the TalentLayer network. This is remitted back to the platform that posted the job.&#x20;

The default configuration of this fee is 0%.&#x20;

### TalentLayer Fee (1%)

This fee is used to support the development of the TalentLayer protocol. It is sent to the TalentLayer treasury. The treasury is currently managed by the TalentLayer Core team and will eventually be transitioned to be managed by the eventual TalentLayer DAO.&#x20;

{% hint style="info" %}
**Market-Based Fee Pricing:** We are in the process of re-working our fee system to allow for platforms to configure Originating Platform Fees, amongst other alternatives. Please standby for updates. This decision was made based on user feedback and game theoretical evaluation.&#x20;
{% endhint %}

## Job Posting Fees

Because many platforms desire to levy fees on job posts, TalentLayer will offer an optional configurable job posting fee. The default Job Posting Fee will be 0%.&#x20;

When considering whether to levy a job posting fee, take into consideration that charging to post jobs can help limit the possibility of spam job posts on your platform.&#x20;

{% hint style="warning" %}
**Alert:** The Job Posting Fee is in development and is launching soon.&#x20;
{% endhint %}

## Gas Fees

By making transactions, your users will experience any gas or transaction fees required by the blockchain you are interfacing with.&#x20;

## Fee Sponsorship

With Fee Sponsorship, you can cover protocol fees and gas fees on behalf of your users. This allows you to create a "fee-less" experience for users.&#x20;

Fee Sponsorship can be configured with your Platform ID and involves you loading a wallet with cryptos to cover fees that users incur.

{% hint style="warning" %}
**Alert:** The Fee Sponsorship is in development and is launching soon.&#x20;
{% endhint %}

## Other Fees and Economics

TalentLayer is currently finalizing our economic model and fee system. We intend to gradually roll out incentives and fees over time alongside our early partners.
