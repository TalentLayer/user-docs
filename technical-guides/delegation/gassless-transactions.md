# Gassless Transactions

## Support for Gasless Meta-transaction

Our contracts are EIP-2771 compatible so they can support meta-transactions. Our implementation follows the standard provided by `@opengsn/contracts`.

### Relayers

In order to enable gassless transactions, platforms building on TalentLayer must choose a relayer and integrate it into their frontend. Platforms are also responsible for managing whitelisting, since we advise only covering gas costs for a subset of trusted users.

{% hint style="warning" %}
Need help choosing a relayer? We're happy to chat about it! Reach out to us on the "contact" page of the documentation.
{% endhint %}

Any relayer solutions which are EIP-2771 compatible work with TalentLayer's contracts.

Our team has vetted a few relayer solutions that we recommend supporting:

* **OpenGSN (V2 or V3)**
  *   Implementation:

      [Open GSN Implementation](https://www.notion.so/Open-GSN-Implementation-ba1cd34a59914ffcaba0537d48f3a130)
  * decentralized, network of relayers, not many but anyone can run their own
  * need to develop Paymaster contract (probably one for each platform which will have a whitelist of users that can be sponsored)
  * expensive, multiple extra things done on chain
* **Biconomy**
  *   Implementation:

      [Biconomy Implementation](https://www.notion.so/Biconomy-Implementation-1d0084455fa64df5861b4b4c9be09a83)
  * semi-centralized, network of relayers, many are Biconomy’s but other people can join?
  * no need to develop any new contracts
* **OZ Defender**
  *   Implementation:

      [OZ Defender Implementation](https://www.notion.so/OZ-Defender-Implementation-75bec36238184eedaf576aa0bd75cf54)
  * centralized, single relayer, they have the private key
  * no need to develop any new contracts
  * need to spin up server or use AutoTask
