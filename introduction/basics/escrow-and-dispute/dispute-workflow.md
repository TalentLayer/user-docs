# Dispute Workflow

## Terminology

* **Dispute:** a disagreement between two (or more) parties
* **Ruling:** a decision taken about the resolution of a dispute
* **Arbitrator:** the entity that has the power to give a ruling
* **Appeal:** an opportunity for a party to try to contest the current (but not final) ruling
* **Evidence:** material provided by a party to support his/her viewpoint

## Dispute Resolution Deep Dive

{% embed url="https://youtu.be/3GlDAjYVC2E" %}
Recorded January 2023 - Subject to Change
{% endembed %}

## Dispute Workflow

1. Two parties disagree on something.
2. They can't reach an agreement. One party submits a request for creating a _dispute._
3. The other party has a period of time to accept the dispute and proceed with its creation by paying the arbitration fee as well. If the time period expires, the dispute will be resolved in favor of the party who requested its creation.
4. If the dispute gets created, each party can submit _evidence_ to show their viewpoint and give reasons why they believe they are right
5. An _arbitrator_ reviews the supporting materials, decides who’s right and gives a _ruling_
6. A period opens in which the parties can _appeal_ the _ruling_ taken by the _arbitrator_
7. The _arbitrator_ considers the _appeals_ and after the appeal period is over takes a final decision, entering the **ruling** (more on this later)

Example: dispute on the execution of a service

1. Alice has hired Bob on HireVibes to create a website for her business. The money is locked in an escrow and will be released to Bob once the job is done and meets Alice’s expectations.
2. When Bob is done with the website, Alice believes that the job was not done sufficiently for Bob to be paid. They disagree on this, so Alice decides to request the creation of a dispute.
3. Bob does not agree with Alice, so he decides to proceed with the creation of the dispute.
4. Both Alice and Bob submit materials to support their point of view
5. HireVibes’ customer support reviews the materials and believes that Alice is right
6. Bob can appeal HireVibes’ decision, giving extra information
7. HireVibes’ still believes that Alice is right and takes a final decision. The escrow is automatically released to Alice

{% hint style="info" %}
**Who is The Arbitrator?** Arbitrators can be either centralized (e.g. the customer support of the platform) or decentralized (e.g. Kleros’ network of jurors). TalentLayer supports two options for Dispute Resolution; Kleros and centralized dispute resolution, which is managed by the platform posting the job.&#x20;
{% endhint %}

## Costs

Arbitrators usually take a fee for ruling on a dispute.

When a party requests the creation of a dispute, it has to lock the arbitration fee in the escrow. In order to accept the dispute, the other party will have to pay the arbitration fee as well. The winner of the dispute will get the arbitration fee reimbursed.

Appeals also have a cost which is defined by the arbitrator.

## Standards

In order to be as modular and interoperable as possible, the dispute resolution implementation follows two of the standards defined for this purpose: the Arbitration and Evidence standards.

{% content-ref url="../../../technical-guides/lower-level-technology/standards/erc-792-arbitration-standard.md" %}
[erc-792-arbitration-standard.md](../../../technical-guides/lower-level-technology/standards/erc-792-arbitration-standard.md)
{% endcontent-ref %}

{% content-ref url="../../../technical-guides/lower-level-technology/standards/erc-1497-evidence-standard.md" %}
[erc-1497-evidence-standard.md](../../../technical-guides/lower-level-technology/standards/erc-1497-evidence-standard.md)
{% endcontent-ref %}



