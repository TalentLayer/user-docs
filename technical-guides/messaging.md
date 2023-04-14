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

### 2. Conversations
The Client can be used to create a conversation with another user, and send messages to this conversation.
A conversation is an object gathering all the contextual data related to a conversation between two users,
as well as functions used to send and receive messages as well as websocket listeners, used to stream incoming messages.

```typescript
export declare class ConversationV2 {
  topic: string;
  keyMaterial: Uint8Array;
  context?: InvitationContext;
  private header;
  private client;
  peerAddress: string;
  constructor(client: Client, invitation: InvitationV1, header: SealedInvitationHeaderV1, peerAddress: string);
  static create(client: Client, invitation: InvitationV1, header: SealedInvitationHeaderV1): Promise<ConversationV2>;
  get createdAt(): Date;
  /**
   * Returns a list of all messages to/from the peerAddress
   */
  messages(opts?: ListMessagesOptions): Promise<DecodedMessage[]>;
  messagesPaginated(opts?: ListMessagesPaginatedOptions): AsyncGenerator<DecodedMessage[]>;
  /**
   * Returns a Stream of any new messages to/from the peerAddress
   */
  streamMessages(): Promise<Stream<DecodedMessage>>;
  /**
   * Send a message into the conversation
   */
  send(content: any, // eslint-disable-line @typescript-eslint/no-explicit-any
       options?: SendOptions): Promise<DecodedMessage>;
  get clientAddress(): string;
  private encodeMessage;
  decodeMessage(env: messageApi.Envelope): Promise<DecodedMessage>;
}

export declare type InvitationContext = {
    conversationId: string;
    metadata: {
      [k: string]: string;
  };
};
```

Example of retrieving a list of a user's conversation:
(The client being already initialized with the user's private key)

```typescript
const listConversations = async (): Promise<Conversation[]> => {
    try {
      const conv: Conversation[] = (await client.conversations.list());
    } catch (e) {
      console.error(e);
    }
    return conv;
    };
```

### 3. Messages
The client object has a “conversations.list()” function, which once called, returns an array of “Conversation” objects:
The conversation object has a “messages()” function, which once called, returns an array of “DecodedMessage” objects:


```typescript
export declare class DecodedMessage {
  id: string;
  messageVersion: 'v1' | 'v2';
  senderAddress: string;
  recipientAddress?: string;
  sent: Date;
  contentTopic: string;
  conversation: Conversation;
  contentType: ContentTypeId;
  content: any;
  error?: Error;
  constructor({ id, messageVersion, senderAddress, recipientAddress, conversation, contentType, contentTopic, content, sent, error, }: DecodedMessage);
  static fromV1Message(message: MessageV1, content: any, // eslint-disable-line @typescript-eslint/no-explicit-any
                       contentType: ContentTypeId, contentTopic: string, conversation: Conversation, error?: Error): DecodedMessage;
  static fromV2Message(message: MessageV2, content: any, // eslint-disable-line @typescript-eslint/no-explicit-any
                       contentType: ContentTypeId, contentTopic: string, conversation: Conversation, error?: Error): DecodedMessage;
}
```

The message itself is stored in “content”.

Example of retrieving a list of conversation's messages:
(The client being already initialized with the user's private key)

```typescript
import {DecodedMessage} from "@xmtp/xmtp-js";

const listMessages = async (): Promise<DecodedMessage[]> => {
  try {
    const messages: DecodedMessage[] = await conversation.messages();
  } catch (e) {
    console.error(e);
  }
  return messages;
};
```


### 4. Sending messages
Sending a message is done through the Conversation object.
The client object has a “conversations.newConversation(peerAddress, context?)” function, which once called, returns a “Conversation” object.
The "context" object is optional, and can be used to add contextual data to the conversation, such as a conversation ID, or any other metadata.
Further details on what TalentLayer implemented can be found in the SDK usage section.

Exemple of sending a message without context:
```typescript
const sendMessage = async (message: string): Promise<DecodedMessage> => {
  const conversation = await client.conversations.newConversation(peerAddress);
  return await conversation.send(message);
};
```


### 5. Websocket listeners
There are 2 websocket listeners available in the SDK:
- “client.conversations.stream()” Available from the client object, which streams incoming conversations to the user
- “conversation.streamMessages()” Specific for each conversation, which streams incoming messages to the user

Example of using the client conversation stream:

```typescript
import {Conversation} from "@xmtp/xmtp-js";

const streamConversations = async () => {
  const stream: Stream<Conversation> | undefined = await providerState.client?.conversations.stream();
  if (!stream) return;
  for await (const conversation: Conversation of stream) {
  // Your logic here
  }
};
```

Example of using the message stream:

```typescript
const streamMessages = async (conversation: Conversation) => {
const stream: Stream<DecodedMessage> | undefined = await conversation.streamMessages();
  if (!stream) return;
  for await (const message: DecodedMessage of stream) {
  // Your logic here
  }
};
```


