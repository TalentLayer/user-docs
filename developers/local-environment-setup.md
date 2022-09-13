---
description: >-
  This guide walks you through setting up our subgraph locally using Docker and
  Hardhat, as well as other local contracts and connections to the Indie Demo
  Dapp.
---

# Local Environment Setup

## Installations&#x20;

Install Docker&#x20;

Update your branches (this is needed to have the last added events and Docker folder)

Add Hardhat RPC in Metamask

## Contract Setup&#x20;

Create a local chain:&#x20;

```
npx hardhat node 
```

Deploy the contract:

```
npx hardhat deploy --use-pohmock --network localhost 
```

Mint a talentLayerId:&#x20;

```
npx hardhat run scripts/playground/mint-ID.ts --network localhost 
```

## Graph Setup

Update manually the json (network.json file) with new contracts addresses and set up startBlock to 0&#x20;

Optional: if your branch was not up to date - run « `npm run codegen` » to have the generated folder

Build the config: update subgraph.yaml:&#x20;

```
graph build --network xdai 

// if the above command don't work use the following
npm run build --network xdai

// check if the network.json address are the same in the subgraph.yaml + startBlock to 0
```

Launch the docker run-graph-node.sh&#x20;

```
//On Windows, bash terminal

sh run-graph-node.sh
```

Deploy the new graph:&#x20;

```
npm run remove-local 
npm run create-local
npm run deploy-local
```

## Indie Dapp Setup&#x20;

Update .env with the following

```
REACT_APP_NETWORK_ID=1337
REACT_APP_SUBGRAPH_URL='http://localhost:8000/subgraphs/name/talentlayer/talent-layer-protocol'
```

&#x20;Update config/app.ts with new contract addresses in const local part&#x20;

```
rpcUrl: http://127.0.0.1:8545/
```

## Common Issues

### xDAI Network Issue

If you have « Xdai network problem » please re launch the run-graph-node.sh&#x20;

### Docker Issue

If you have a docker problem, please check that you launch your hardhat node before the docker containers

### Gluegun Problem&#x20;

If you have a problem with gluegun problem, please run:&#x20;

```
npm i -D gluegun
```

If you have any other issues, please reach out to our team on Twitter @Talentlayer.&#x20;
