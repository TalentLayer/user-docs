# Native Integration

## TalentLayer as a Backend

Platforms that choose Native Integration opt to use TalentLayer as a backend for their platform, where all supply and demand is listed at the network level for cross-platform deals.

Native Integration is good for teams who may:

* want to have 100% of their current supply and demand listed on the network for cross-platform transactions
* don't have an existing user account system, payments system, or dispute resolution
* are adding marketplace features into an app in a different vertical
* don't want to custody user data for GDPR reasons
* want to avoid building a backend from scratch, to go to market faster

All of your users and service requests will be listed on the network as available supply and demand; any other platform on the network can propose cross-platform transactions with your users.&#x20;

With Native Integrations, each user on your platform has an reputation and profile at the network level that can be viewed by and used on other platforms.&#x20;

{% hint style="info" %}
**Native Integration** is available today, with extensive documentation, code examples, and more.
{% endhint %}

### On-Demand Integration - TalentLayer for Supplimenting Supply & Demand

Platforms that choose On-Demand Integration opt to use TalentLayer to supplement existing supply and demand on their marketplace.

On-Demand Integration is good for teams who may:

* want to list only excess supply and demand on the network for cross-platform transactions
* already have an existing user account system, payments system, or dispute resolution
* want to maintain custody of their own user's profiles and their current network effect

When you lack supply or demand for a specific category of service, you can pull in resources from the network on demand.&#x20;

> **On-Demand Fulfillment Workflow**\
> \
> Marketplace A has insufficient supply of Python developers to meet the demand of Python gigs available on their platform. \
> \
> Marketplace A pushes current available Python gigs to the network via TalentLayer API. \
> \
> Marketplace A receives proposals from users across the network, which it then displays to the hirers on it's platform. \
> \
> Hirers select the winning candidate and complete the transaction. Payment remittance is triggered on Marketplace A by the hirer and facilitated by TalentLayer. \
> \
> The candidate receives payment on the platform they are using.

All of your users and service requests will remain custodied by your platform in whatever manner they are today. There will be no network-native representation of your users available for other platforms to view or display.&#x20;

{% hint style="warning" %}
**On-Demand Integration** is a feature of the TalentLayer Abstracted API and SDK. While it is possible to build a platform with On-Demand Integration today, this implementation pattern is not documented and has no example code available.&#x20;
{% endhint %}
