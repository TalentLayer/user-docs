# Escrow & Dispute System

The TalentLayer Escrow and Dispute Resolution Module allows for secure payments between users on TalentLayer integrated marketplaces AND between TalentLayer integrated marketplaces. TalentLayer's Escrow and Dispute Resolution allows for users on different marketplaces to remit transactions and handle disputes associated with [specific Jobs.](jobs-and-proposals.md)&#x20;

## Escrow

The TalentLayer Escrow System is an adaptation of [Kleros's MultipleArbitrableTransaction.sol](https://github.com/kleros/kleros-interaction/blob/master/contracts/standard/arbitration/MultipleArbitrableTransaction.sol) smart contract and Yubiai's [MultipleArbitrableTransaction.sol](https://github.com/yubiai/yubiai-contracts/blob/main/contracts/MultipleArbitrableTransaction.sol) updated version. T

### Escrow Capabilities

It is possible for escrow to be released in part to the counter-party by the employer. This feature allows for things like milestone-based projects; where based on the delivery of certain sub-jobs, an employee can receive payments. This also enables periodical payment of hourly work; for example, weekly pay for hours worked.

Escrow contracts can not currently be refilled after the full amount has been released. After the full amount has been released, the job will automatically be marked complete and prompt the users to leave a review. Future transactions will have to be completed in a subsequent job.

It is possible for a freelancer to voluntarily opt-out of a job and be compensated partially for work completed, with the employer receiving the remaining amount of escrow back to their own wallet.

### TalentLayer Escrow With or Without Disputes

At the platform level, you can decide whether to allow your users to initiate disputes via Kleros or not. If you choose to allow for disputes via Kleros, handling of the release of escrow after a dispute has been judged is automatically completed by the contracts.&#x20;

{% hint style="info" %}
**Alternative Dispute Resolution Protocols:** TalentLayer aims to eventually allow integrated platforms to interface easily with an array of decentralized dispute resolution protocols. Kleros is currently the industry leader in decentralized dispute resolution and was therefore an obvious first choice.&#x20;
{% endhint %}

## Disputes

Through leveraging an augmented version of Kleros Escrow, TalentLayer's escrow system is fully compatible with the Kleros decentralized dispute resolution protocol. When one user initiates a dispute, the result of the dispute is judged by jurors in the Kleros Court system. A ruling is then sent back to the platform, to be displayed to the users.

By having decentralized multi-party juror dispute resolution, TalentLayer allows marketplaces to avoid the common pitfalls that come with centrally managed dispute resolutions; namley, biased decisions, high cost of resolution, and inefficiency.&#x20;

### Learn About Kleros

{% embed url="https://kleros.io/" %}

### How does Kleros Court work?

Once a dispute has been initiated via TalentLayer, on the backend your dispute gets sent to Kleros Court. The lifecycle of disputes follows a five, step process.&#x20;

> A dispute goes through several stages after (it) is created:
>
> 1. **Evidence** - Evidence can be submitted. This is also when drawing has to take place.
> 2. **Commit** - Jurors commit a hashed vote. This is skipped for courts without hidden votes.&#x20;
> 3. **Vote -** Jurors reveal/cast their vote depending on whether the court has hidden votes or not.&#x20;
> 4. **Appeal** - **** The dispute can be appealed.&#x20;
> 5. **Execution** - Tokens are redistributed and the ruling is executed.
>
> The period of each stage is different for each (sub)court.
>
> From "What Happens During a Dispute" on [Kleros.Gitbook.io](https://kleros.gitbook.io/docs/products/court/what-happens-during-a-dispute)





