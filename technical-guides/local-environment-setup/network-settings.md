---
description: Setup guides for specific networks
---

# Network Settings

## Indie Frontend

| Network       | Status                     | Docs                                                                                 |
| ------------- | -------------------------- | ------------------------------------------------------------------------------------ |
| Gnosis / xDAI | Deployed                   | [https://docs.gnosis.io/protocol/](https://docs.gnosis.io/protocol/)                 |
| Ethereum      | Pending (On Testnet)       | [https://ethereum.org/en/developers/docs/](https://ethereum.org/en/developers/docs/) |
| Aurora        | Pending (Winter 2022-2023) | [https://doc.aurora.dev/](https://doc.aurora.dev/)                                   |

Currently TalentLayer Indie only supports the xDAI network.

## Goerli

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
