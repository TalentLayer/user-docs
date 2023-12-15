# ERC-792: Arbitration standard

## About The Standard

{% embed url="https://github.com/ethereum/EIPs/issues/792" %}

Defines a contracts standard for arbitration. Specifically, defines two types of contracts:

* **`Arbitrable` contracts:** where disputes can arise (e.g. an escrow contract)
* **`Arbitrator` contracts:** used to resolve disputes.

Every `Arbitrable` contract can be adjudicated by every `Arbitrator` contract The standard defines the way that `Arbitrable` and `Arbitrator` contracts should interact with each other.

Using two contracts allows separation between the ruling and its enforcement. In this way, an arbitrable app can easily switch from one arbitration service to another one with no breaking changes.



## Arbitrator

{% embed url="https://github.com/kleros/erc-792/blob/master/contracts/IArbitrator.sol" %}

**Functionalities:**

* allow dispute creation (`createDispute` function, must be called by the `Arbitrable` contract)
* allow to appeal a ruling (`appeal` function, must be called by the `Arbitrable` contract)
* allow giving rulings (by calling the `rule` function of the `Arbitrable` contract)

**Arbitration costs:**

The creation of a dispute has a cost to be paid to the arbitrator. Appeals also have a cost.

To create a dispute, both parties should pay the arbitration fee. Whoever wins the dispute should get the funds and should get reimbursed for the arbitration fee.

_E.g.: if the arbitration cost is C, both parties will pay C to create a dispute summing up to a total of 2C paid in fees. Half of the fees (C) will go to the arbitrator and the other half (C) will be reimbursed to the winner of the dispute_

**Appeals:**

It is up to the arbitrator to decide whether or not to allow appeals:

* no appeals: the ruling given by the arbitrator should be immediatly final
* with appeals: after a ruling is given an appeal period opens, in which parties can appeal the current decision.

Also, it is up to the arbitrator to define how to handle appeal periods and what happens when an appeal is received.

_An example could be: after a decision is taken the parties have some time to appeal the decision. If no one appeals within this timeframe then the decision becomes final, otherwise the arbitrator has to take a decision again (which can be the same one as before) until no one appeals. Appealing has a cost so parties won't do it forever if that doesn't change the arbitrator's mind._

However, arbitrators should only give a final ruling (call `rule` on the `Arbitrable` contract) when all appeals are exhausted.

**Dispute status:**

* `Waiting`: the dispute is this status when it gets created
* `Appealable`: the dispute got a _ruling_ and the `Arbitrator` allows to _appeal_ it.
* `Solved`: the dispute got a _**ruling**_ and the **ruling** is final. This doesn’t imply that the ruling has been enforced, it just means that the decision on the dispute is final and to be executed.
  * if a dispute is not appealed within the appealing time period, it becomes `Solved`

## Arbitrable

{% embed url="https://github.com/kleros/erc-792/blob/master/contracts/IArbitrable.sol" %}

**Functionalities**

* determines in which cases a dispute occurs, defining logic to create disputes (by calling `createDispute` on the `Arbitrator` contract and paying the required fee)
* determines in which cases appeal is possible, defining logic to appeal disputes (by calling `appeal` on the `Arbitrator` contract and paying the required fee)
  * Note: it just defines in which situation it would be possible to appeal a dispute, based on the context of the arbitrable dApp. It still depends on the arbitrator to decide whether to allow appeals or not.
* enforces decisions given by the `Arbitrator` contract (`rule` function, must be called by the `Arbitrator` contract)

#### Workflow

* The `Arbitrable` contract calls `createDispute` on the `Arbitrator` contract to create a dispute.
* The `Arbitrator` contract gives a ruling. The appeal period opens.
* Appeal is done through the `Arbitrable` contract calling `appeal` on the `Arbitrator` contract
* When the appeal period is over the `Arbitrator` contract gives a final ruling, calling `rule` on the `Arbitrable` contract
* The `Arbitrable` contract enforces the ruling
