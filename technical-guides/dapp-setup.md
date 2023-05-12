# DAPP Setup - Indie

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
NEXT_PUBLIC_WALLECT_CONNECT_PROJECT_ID=xxxxx
NEXT_PUBLIC_NETWORK_ID=80001
NEXT_INFURA_ID=xxxxx
NEXT_INFURA_SECRET=xxxxx
NEXT_PUBLIC_PLATFORM_ID=4
NEXT_PUBLIC_LENS_URL=https://api.lens.dev/
NEXT_PUBLIC_IPFS_BASE_URL=https://ipfs.io/ipfs/
NEXT_PUBLIC_POH_SUBGRAPH_URL=https://api.thegraph.com/subgraphs/name/kleros/proof-of-humanity-mainnet
NEXT_PUBLIC_SISMO_GRAPH_API=https://api.sismo.io/
NEXT_PUBLIC_SIGNATURE_API_URL=https://api.defender.openzeppelin.com/autotasks/4b1688f9-01a4-435d-89ae-d05e0aa0a53b/runs/webhook/b9818d77-3c43-4c3d-bfb8-4c77036de92f/ACXhXsQoCKP8zZVE26gFbh
NEXT_PUBLIC_BACKEND_RPC_URL=https://rpc-mumbai.maticvigil.com/v1/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
{% endcode %}

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
