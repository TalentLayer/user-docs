# Escrow & Dispute System

The TalentLayer Escrow and Dispute Resolution Module allows for secure payments between users on TalentLayer integrated marketplaces AND between TalentLayer integrated marketplaces. TalentLayer's Escrow and Dispute Resolution allows for users on different marketplaces to remit transactions and handle disputes associated with [specific Jobs.](jobs-and-proposals.md)&#x20;

## Escrow

The TalentLayer Escrow System is an adaptation of [Kleros's MultipleArbitrableTransaction.sol](https://github.com/kleros/kleros-interaction/blob/master/contracts/standard/arbitration/MultipleArbitrableTransaction.sol) smart contract and Yubiai's [MultipleArbitrableTransaction.sol](https://github.com/yubiai/yubiai-contracts/blob/main/contracts/MultipleArbitrableTransaction.sol) updated version. T

### Escrow Capabilities

It is possible for escrow to be released in part to the counter-party by the employer. This feature allows for things like milestone-based projects; where based on the delivery of certain sub-jobs, an employee can receive payments. This also enables periodical payment of hourly work; for example, weekly pay for hours worked.

Escrow contracts can not currently be refilled after the full amount has been released. After the full amount has been released, the job will automatically be marked complete and prompt the users to leave a review. Future transactions will have to be completed in a subsequent job.

It is possible for a freelancer to voluntarily opt-out of a job and be compensated partially for work completed, with the employer receiving the remaining amount of escrow back to their own wallet.

## Disputes

Documentation coming soon.
