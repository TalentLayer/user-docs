# Integrating XMTP

When studying a service or a proposal, it is important for users to be able to communicate with the author. TalentLayer provides an integration example of XMTP, a messaging system that allows users to communicate with each other using their ETH address. This guide will show you how to integrate the XMTP messaging system into your DAPP.


## Techincal overview

XMTP is based on asymmetric encryption. When u user signs up using his ETH address, he is prompted to use his wallet signature to generate a pair of Private/Public keys. The private key is stored on chain, and requires the user's wallet signature to be retrieved; whereas the public key is stored publicly on chain.
The public key is available to other XMTP users who wish to communicate with this user, and is used to encrypt messages before sending them. The private key is used to decrypt messages.
The sender's public key is included in the message so that the recipient can verify the sender's identity.


## Workflow

When registering to XMTP, wallet signature is required to register the wallet as a User.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db9ea7e9-d35b-4d43-8227-7ebb862dac8e/Untitled.png)

(This will be asked only once).

Then for each login, a wallet signature will be asked to decrypt this Private Key and create an XMTP client based on this key.
Messages are stored on XMTP private nodes for now, but will be stored in a decentralized manner in a near future.

## SDK analysis
XMTP provides a [complete SDK](https://xmtp.org/docs/client-sdk/javascript/concepts/intro-to-sdk) to interact with the XMTP protocol.



### 1. Client
All calls to XMTP protocol are done through the XMTP [Client](https://xmtp.org/docs/client-sdk/javascript/reference/classes/Client):
This Client is used to retrieve the keys of the user using his wallet signature, and use them to initialize a functional client that can be used to send and receive messages.

```typescript
import { Client } from '@xmtp/xmtp-js';

const keys = await Client.getKeys(signer, { env: 'production' });
const client = await Client.create(null, {
  env: 'prod',
  privateKeyOverride: keys,
});
```

