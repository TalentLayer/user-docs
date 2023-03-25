# DAPP Setup

"Indie" is an open-source fork-able marketplace codebase that is available for marketplaces and other platforms integrating with [TalentLayer](https://docs.talentlayer.org/) to borrow from and use to get inspired.

It's a good first step to set up a local version of Indie to...

1. Get to know how frontends interface with TalentLayer
2. Optionally, use Indie as a foundation for your next DAPP.

## Explore the DAPP

We've hosted a version of Indie on Mumbai testnet for you to play around with! Have fun.

{% embed url="https://indie-two.vercel.app/" %}

## Watch the Demo

{% embed url="https://youtu.be/8Y6E282Nwtc" %}

## View on Github&#x20;

{% embed url="https://github.com/TalentLayer-Labs/indie-frontend" %}

## Local Setup Instructions

### 1. Clone Repository from GitHub

```bash
git clone https://github.com/TalentLayer-Labs/indie-frontend
```

### 2. Move to directory

```bash
cd indie-frontend
```

### 3. Setup .env File

```bash
touch .env #Create env file
```

{% code title=".env" lineNumbers="true" %}
```
VITE_WALLECT_CONNECT_PROJECT_ID=xxxxx
VITE_NETWORK_ID=80001
VITE_INFURA_ID=xxxxx
VITE_INFURA_SECRET=xxxxxx
VITE_PLATFORM_ID=4
VITE_LENS_URL=https://api.lens.dev/
VITE_IPFS_BASE_URL=https://ipfs.io/ipfs/
VITE_POH_SUBGRAPH_URL=https://api.thegraph.com/subgraphs/name/kleros/proof-of-humanity-mainnet
VITE_SIGNATURE_API_URL=
```
{% endcode %}

* Get the VITE\_WALLECT\_CONNECT\_PROJECT\_ID from  [https://walletconnect.com/](https://walletconnect.com/)
* Get the VITE\_INFURA\_ID and VITE\_INFURA\_SECRET at [https://www.infura.io/](https://www.infura.io/) by creating a new project for IPFS.
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
