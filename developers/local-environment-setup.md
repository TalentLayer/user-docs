---
description: >-
  This guide walks you through setting up our subgraph locally using Docker and
  Hardhat, as well as other local contracts and connections to the Indie Demo
  Dapp.
---

# Local Environment Setup

## Requirements &#x20;

→ Git clone or Update your branches

```
git clone https://github.com/TalentLayer/talentlayer-id-contracts.git
```

```
git clone https://github.com/TalentLayer/talentlayer-id-dapp.git
```

```
git clone https://github.com/TalentLayer/talentlayer-id-subgraph.git
```

→ Run `npm i` in each folder

→ Install docker ([https://www.docker.com/](https://www.docker.com/))

## Contract folder Setup&#x20;

{% hint style="info" %}
In the [talentlayer-id-contracts](https://github.com/TalentLayer/talentlayer-id-contracts)
{% endhint %}

→ Please read and fill the **.env** file with your information

For local setting, ETHERSCAN\_API\_KEY & GNOSIS\_API\_KEY are optional

→ Create a local chain:&#x20;

```
npx hardhat node 
```

→ Run&#x20;

```
make install
```

Please read the Makefile in you need information on the deployment process



## Indie Subgraph folder Setup&#x20;

{% hint style="info" %}
In the [talentlayer-id-subgraph](https://github.com/TalentLayer/talentlayer-id-subgraph)
{% endhint %}

→ Launch the docker run-graph-node.sh&#x20;

```
sh run-graph-node.sh
```

→ Run &#x20;

```
make regenerate
```



## Dapp folder Setup

{% hint style="info" %}
In the [talentlayer-id-dapp](https://github.com/TalentLayer/talentlayer-id-dapp)
{% endhint %}

→ Update .env with the following

```
REACT_APP_NETWORK_ID=1337
REACT_APP_SUBGRAPH_URL='http://localhost:8000/subgraphs/name/talentlayer/talent-layer-protocol'
```

{% hint style="info" %}
localhost = 1337 / Mainnet = 1 / Gnosis = 100 / Kovan = 42 / Goerli =5
{% endhint %}

→ run

```
npm run start
```

## Others networks

Please find below the changes to apply before launching all the installation commands&#x20;

For Goerli network

{% hint style="info" %}
In the [talentlayer-id-contracts](https://github.com/TalentLayer/talentlayer-id-contracts)
{% endhint %}

→ Duplicate the `talent.config_localhost.json` file & Rename it in `talent.config_goerli.json`

→ In the .env file, please replace **localhost** by **goerli** on the `DEPLOY_NETWORK` variable

{% hint style="info" %}
In the [talentlayer-id-dapp](https://github.com/TalentLayer/talentlayer-id-dapp)
{% endhint %}

→ In the .env file, please change the REACT\_APP\_NETWORK\_ID with 5 (goerli)

→ In the config > app.ts please add

```
import configGoerli from '../autoconfig/talent.config_goerli.json';
```

## Support

If you have any other issues or need help, please reach out to our team on Twitter @Talentlayer.&#x20;
