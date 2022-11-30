# 🛠 Integration

## Indie Frontend

The indie frontend is a [codebase](https://github.com/TalentLayer-Labs/indie-frontend) provided by us for quickly building a platform integrating the TalentLayer tools enabling the interoperability with any other integrating platform. Find out how to set up the indie frontend on your local environment[ here](technical-guides/local-environment-setup/indie-frontend.md)!

## Using the SDK

We are currently working on an SDK to help platforms integrate efficiently. Stay up to date on the progress by following us on [Twitter @TalentLayer](https://twitter.com/TalentLayer).

## We're Here to Help

Since TalentLayer Core is currently in **Alpha,** we recommend reaching out to the team on Twitter @TalentLayer before integrating directly with TalentLayer’s interoperable reputation and services systems.

We are happy to help you:

1. Understand how to implement TalentLayer on your platform: Every platform is a little different, and we want to know how we can best make our tech stack as composable as possible. By helping you, we learn too!
2. Deploy TalentLayer on your platform’s native EVM chain: TalentLayer aims to be a cross-chain platform, and are in the process of spinning up implementations of our Alpha release on multiple EVM chains.

{% hint style="danger" %}
**October Metadata Update:** Please be aware of our **metadata update** that took place in October 2022. To guarantee that your implementation will interface with the TalentLayer interoperable services repository and/or reputation system you must update your system to the V3 of our data model. The previous versions of our data schemas do not include a key identifier that represents originating marketplaces/platforms - something necessary for the TalentLayer contracts to know the difference between the various actors writing data to TalentLayer. All future data schema updates should not impact interoperability.
{% endhint %}
