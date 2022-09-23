# What is TalentLayer Core?

{% hint style="info" %}
**Good to know:** TalentLayer is currently in Pre-Alpha. We are live on Gnosis Mainnet and various ETH Testnets. If you have questions on integrating, get in touch with us on [Twitter @TalentLayer.](https://twitter.com/TalentLayer)
{% endhint %}

TalentLayer Core is composable, decentralized, open-source infrastructure for talent markets; allowing anyone to easily build interoperable gig marketplaces. It is designed to empower workers to own their own reputation and access jobs without limitation. TalentLayer’s Alpha is currently in development.

TalentLayer Core is composed of the following key modules:

* [TalentLayer Universal Work Reputation Module ](broken-reference)\[live 07/24/2022]
  * [TalentLayer ID System](work-reputation-module/what-is-talentlayer-id.md)
  * [TalentLayer Review System](work-reputation-module/reviews-and-reputation.md)
* [TalentLayer Universal Work Facilitation Module](broken-reference) \[live 07/24/2022]
  * [TalentLayer Universal Job & Proposal System](work-facilitation-module/jobs-and-proposals.md)
  * [TalentLayer Escrow & Dispute System](work-facilitation-module/escrow-and-dispute-system.md)

TalentLayer creates a paradigm shift in how freelance marketplaces operate by creating a universal reputation system and jobs repository that any marketplace can tap into. Users maintain one self-owned reputation across many marketplaces. Marketplaces that build on TalentLayer receive rewards by onboarding talent and jobs.

## Integrating TalentLayer

### Exploring TalentLayer Modules

TalentLayer's three core modules can be integrated with your platform based on your needs. For example, it is possible to integrate TalentLayer's Universal Reputation Module but not TalentLayer's Escrow & Dispute Resolution Module.&#x20;

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### Integration Quick-Start Guides

TalentLayer is ready to help you build the next generation of work platforms as well as integrate into existing platforms. Check out our integration guides to learn more.&#x20;

{% content-ref url="integration-guides/existing-platforms.md" %}
[existing-platforms.md](integration-guides/existing-platforms.md)
{% endcontent-ref %}

{% content-ref url="integration-guides/new-platforms.md" %}
[new-platforms.md](integration-guides/new-platforms.md)
{% endcontent-ref %}

{% hint style="danger" %}
**Metadata V3:** To guarantee that your implementation will interface with the TalentLayer interoperable jobs repository and/or reputation system you must update your system to the V3 of our data model; coming soon (October 2022). The existing data schema does not include a key identifier that represents originating marketplaces/platforms - something necessary for the TalentLayer contracts to know the difference between the various actors writing data to TalentLayer. All future data schema updates should not impact interoperability. Thank you for your patience as we work towards our interoperable system!
{% endhint %}

### Meet TalentLayer

Get to know TalentLayer's vision by visiting our website:

{% embed url="https://www.talentlayer.org/manifesto.php" %}
TalentLayer's website.
{% endembed %}
