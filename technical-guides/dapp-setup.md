# DAPP Setup

"Indie" is an open-source fork-able codebase that is available for marketplaces and other platforms integrating with [TalentLayer](https://docs.talentlayer.org/) to borrow from and use to get inspired.

It's a good first step to set up a local version of Indie to...

1. Get to know how frontends interface with TalentLayer
2. Optionally, use Indie as a foundation for your next DAPP.

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
VITE_WALLECT_CONNECT_PROJECT_ID=
VITE_NETWORK_ID=
VITE_INFURA_ID=
VITE_INFURA_SECRET=
VITE_SUBGRAPH_URL=
VITE_PLATFORMID=
```
{% endcode %}

Get the WALLET\_CONNECT\_PROJECT\_ID from  [https://walletconnect.com/](https://walletconnect.com/)

Get the INFURA\_ID and INFURA\_SECRET at [https://www.infura.io/](https://www.infura.io/) by creating a new project for IPFS.

Set NETWORK\_ID to for now 5, this is the ID of [goerli testnet](https://goerli.net/). For other networks, find the chainID on [Chainlist](https://chainlist.org/).&#x20;

Set the SUBGRAPH\_URL to [https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol](https://api.thegraph.com/subgraphs/name/talentlayer/talent-layer-protocol). \
(This is the subgraph endpoint on goerli testnet. The available endpoints can be found in the [Graph Schema](local-environment-setup/talentlayer-id-subgraph/graph-schema.md) page.)

If you have a PLATFORMID, set it to the numeric identifier for your ID.&#x20;

If you do not yet have a PLATFORMID, set this field  to 1.  This allows you to interface with the contracts as a null identity on testnet while you are waiting for your PLATFORMID.&#x20;

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
