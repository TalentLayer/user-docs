# Demo DAPP Setup - StarterKit

<figure><img src="../.gitbook/assets/Screenshot 2023-08-08 at 5.43.21 PM.png" alt=""><figcaption></figcaption></figure>

"StarterKit" is an open-source fork-able mobile-first marketplace codebase that is a great starting point for teams building on TalentLayer. StarterKit was adapted from the Indie starter codebase, with additional improvments to make it mobile-first.

It's a good first step to set up a local version of StarterKit to...

1. Get to know how frontends interface with TalentLayer
2. Optionally, use Indie as a foundation for your next DAPP.

## Explore the DAPP

We've hosted a version of StarterKit on Mumbai testnet for you to play around with! Have fun.

{% embed url="https://starter-kit-xmtp-tl.vercel.app/" %}

## View on Github&#x20;

{% embed url="https://github.com/TalentLayer-Labs/indie-frontend" %}

## Local Setup Instructions

### 1. Clone Repository from GitHub

```bash
git clone https://github.com/TalentLayer-Labs/starter-kit
```

### 2. Move to directory

```bash
cd starter-kit
```

### 3. Setup .env File

Setup your local environnement by copying the .env.example and adjust the variables.

* Get the NEXT\_WALLECT\_CONNECT\_PROJECT\_ID from  [https://walletconnect.com/](https://walletconnect.com/)
* Get the NEXT\_INFURA\_ID and VITE\_INFURA\_SECRET at [https://www.infura.io/](https://www.infura.io/) by creating a new project for IPFS.
* Set NETWORK\_ID to for now to the ID for Mumbai Testnet. Find the chainID on [Chainlist](https://chainlist.org/).&#x20;
* Set it to the numeric identifier for the platform ID you want to post on.&#x20;

Learn about how to request a PLATFORMID here:&#x20;

{% content-ref url="../basics/elements/platformid.md" %}
[platformid.md](../basics/elements/platformid.md)
{% endcontent-ref %}

### 4. Install dependencies

```bash
npm i
```

### 5. Run the dapp!

```bash
npm run dev
```
