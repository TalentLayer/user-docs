# What is Indie?

Indie is a demo DAPP that allows platforms to see how frontends can be integrated with TalentLayer Core.

The TalentLayer team created Indie to serve as a fork-able base for a marketplace that anyone can take, iterate on, and borrow components from to interact with the TalentLayer protocol. Over time, we will be shipping updates to Indie to improve UI and expand its functionality as new features launch on TalentLayer.&#x20;

The Indie demo DAPP is styled as a reputation tool for independent freelancers. Similar to how you can build up a reputation over time by completing work and receiving reviews on freelancing platforms like Upwork or [Freelancer.com](http://freelancer.com), now you and your independent clients can create verified reviews to signal one another’s trustworthiness.

All TalentLayer and TalentLayer Indie components are available on Github with an Apache 2.0 license.&#x20;

## Current Constraints & Status

{% hint style="info" %}
**Good to know:** TalentLayer Indie is currently in testing. If you have bugs to report, please reach out to us on Twitter at @TalentLayer
{% endhint %}

Indie is still in development. The following is a list of the current status of what components are live.

### Component Status

| Feature           | Frontend    | Backend          |
| ----------------- | ----------- | ---------------- |
| Identity creation | Live        | Live             |
| Identity recovery | In Progress | Ready to Go Live |
| Job creator       | Live        | Live             |
| Review system     | Live        | Live             |
| Reputation Search | Live        | In Progress      |
| Escrow system     | Live        | Live             |
| Dispute system    | Live        | In Progress      |

### Known Bugs & Build Issues

#### Proof of Humanity Checker

The POH address validator that is live now is still connected with our testing contract.  Instead of linking our contracts to the real POH contract, we created a fake POH contract where we could manually register people for testing. It's just a matter of switching contract addresses to make it work live.&#x20;

\
Solution: The "associate POH" system is not going to work for you on the current site. Please click "skip verification".

#### Reload Glitch

About: When you re-load a page, sometimes it throws an error saying "page not found".&#x20;

Solution: Go back to the home page and re-try whatever page you were trying to get to.&#x20;

#### Account Recovery Function

About: The "recover account" button on the home page doesn't lead anywhere because the frontend isn't done yet.&#x20;

Status: The backend for recovery via Proof of Humanity is built, just not live yet. We are waiting on the front end to implement this.&#x20;

#### Search Reputation Function

About: Right now the frontend for "search reputation" only shows all reputation updates ever to be made for anyone (displayed in a sort of running list).&#x20;

Status: We just need to update the Graphql request on the backend and plug it into the front end to make this functional.

## Explore Indie

{% embed url="https://www.indie.talentlayer.org" %}

## Guides: Jump right in

Follow our handy guides to get started on the basics as quickly as possible:

{% content-ref url="user-guides/creating-your-talentlayer-id.md" %}
[creating-your-talentlayer-id.md](user-guides/creating-your-talentlayer-id.md)
{% endcontent-ref %}

{% content-ref url="user-guides/creating-your-first-job.md" %}
[creating-your-first-job.md](user-guides/creating-your-first-job.md)
{% endcontent-ref %}

{% content-ref url="user-guides/leaving-mutual-reviews.md" %}
[leaving-mutual-reviews.md](user-guides/leaving-mutual-reviews.md)
{% endcontent-ref %}

## Fundamentals: Dive a little deeper

Learn the fundamentals of TalentLayer to get a deeper understanding of our main features:

{% content-ref url="work-reputation-module/what-is-talentlayer-id.md" %}
[what-is-talentlayer-id.md](work-reputation-module/what-is-talentlayer-id.md)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="work-reputation-module/reviews-and-reputation.md" %}
[reviews-and-reputation.md](work-reputation-module/reviews-and-reputation.md)
{% endcontent-ref %}
