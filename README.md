# What is TalentLayer Core?

{% hint style="info" %}
**Good to know:** TalentLayer is currently in development.&#x20;
{% endhint %}

TalentLayer Core is composable, decentralized, open-source infrastructure for talent markets; allowing anyone to easily build interoperable gig marketplaces. It is designed to empower workers to own their own reputation and access jobs without limitation. TalentLayer’s Alpha is currently in development.

TalentLayer Core is composed of the following key components:

* TalentLayer ID Universal Reputation System \[live]
* TalentLayer Universal Jobs System \[live]
* Escrow System \[not live]
* Decentralized Dispute Resolution System \[not live]

TalentLayer creates a paradigm shift in how freelance marketplaces operate by creating a universal reputation system and jobs repository that any marketplace can tap into. Users maintain one self-owned reputation across many marketplaces. Marketplaces that build on TalentLayer receive rewards by onboarding talent and jobs.

### Integrate TalentLayer

Currently, TalentLayer's identity system and jobs system are live in production - they are actively being updated with improvements. The first live implementation of these systems in a platform can be found here: an independent freelancer reputation tool, [TalentLayer Indie](<README (1).md>).&#x20;

The current version of TalentLayer Core is most suitable for use in platforms that already have an escrow system. If you want to integrate TalentLayer's identity system but you do not already have an escrow system, we recommend integrating Kleros's escrow system, which can be found [here](https://github.com/kleros/escrow). TalentLayer's eventual identity system will be based on Kleros, and if you build an integration with their standard, it will be easily updated to the TalentLayer escrow system upon release.

To guarantee that your implementation will interface with the TalentLayer interoperable jobs repository and/or reputation system you must update your system to the V2 of our data model; coming soon (end of August 2022). The existing data schema does not include a key identifier that represents originating marketplaces/platforms - something neccessary for the TalentLayer contracts to know the difference between the various actors writing data to TalentLayer. All future data schema updates should not impact interoperability.

Thank you for your patience as we work towards our interoperable system!

### Meet TalentLayer

Get to know TalentLayer's vision by visiting our website:

{% embed url="https://www.talentlayer.org/manifesto.php" %}
TalentLayer's website.
{% endembed %}
