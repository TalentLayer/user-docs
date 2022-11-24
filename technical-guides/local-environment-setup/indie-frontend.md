# Indie Frontend

## Requirements

{% hint style="info" %}
Before you continue, make sure your system fulfills the requirements in the [Local Environment Setup](https://app.gitbook.com/o/uoAYI2Mv1g6UqAhiHLVU/s/LxwTmt3MOuMIlBTH8NKY/\~/changes/ea66kIRjVFnvwwnI8she/guides/local-environment-setup).
{% endhint %}

## Instructions

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
(This is the subgraph endpoint on goerli testnet. The available endpoints can be found in the [Graph Schema](talentlayer-id-subgraph/graph-schema.md) page.)

Set PLATFORMID to 1 for now. More info on this will come.

### 4. Install dependencies

```bash
npm i
```

### 5. Run the dapp!

```bash
npm run dev
```
