---
description: Guide on setting up web3email notifications with TalentLayer
---

# Iexec - Web3Mail

## 1. Introduction

### 1.1 What is Iexec & Web3mail?

IExec is a decentralized compute network that been privacy-focused from day 1 — leveraging confidential computing techniques to enable private data to be processed on untrusted remote servers. The team at IExec developed a tool enabling private email sending leveraging their technology — Web3 Mail.

{% embed url="https://tools.docs.iex.ec/tools/web3mail" %}
Iexec Web3mail docs
{% endembed %}

Web3Mail allows platforms to send emails to a user without disclosing his email address. A user can decide to encrypt his email and & allow a platform to send him emails using solely an Ethereum address. The user can decide to revoke this access at any time, or define in advance how many emails he allows the platform to send him. Users to control who can email them and on what terms

Platforms can also enable their own users to send emails to one another, without the users knowing each others email addresses.

Users can “allow” and “disallow” certain senders or demographics of senders (i.e. “I want to only receive outreach from platforms I’ve posted jobs on” or “I want to only receive outreach from hirers who have paid other freelancers successfully”)

They can put up configurable paywalls (i.e. “If someone wants to email me, charge them $0.05 per email” or “If someone wants to email me charge them $0.50 per email, except if the user is a member of Developer DAO”

### 1.2 Why web3mail and TalentLayer?

So far, in enterprise-grade and mainstream consumer facing applications of blockchain technology, user experience and user autonomy/privacy have become polarizing goals; it seems like both can't be achieved at the same time.

One of the best examples of this is how communications with users is handled. Nowadays, personal email is nearly always required to access a decentralized social media, centralized wallet, web 3 hiring platform etc.

The reason that these projects need to gather emails is because, today, email remains the most reliable way to reach users, however this can lead to adverse effects which discourage users to provide their personal email to platforms, such as:

* Users being inadvertently spammed by the platform
* Users being spammed by third parties who managed to get hold of their email (hacks, leaks...)
* Users incentivized to use a fake email to preserve their privacy
* Regulatory issues regarding the use of personal data with GDPR

At TalentLayer, every platform that is building hiring tech using our toolkit needs reliable ways to talk with users regarding events such as Alerts on job postings, payment alerts, promotions etc.

Email being the most reliable way to reach users, we decided to integrate Iexec's web3mail technology in order to allow platforms to send emails to users without disclosing their email address.

***

## 2. Technical Overview

TalentLayer integrated Iexec Web3mail tech by giving a choice to a user to let a platform send him emails for a set of different notifications types to which he can subscribe and unsubscribe anytime he wants. Notification preferences are set in TalentLayer user's metadata.

### 2.1 Workflow

In order to receive email notifications, the user first has to protect (encrypt) his email using Iexec's DataProtector. Then he will grant access to his encrypted email to a platform (represented by the Ethereum Address of the platform's owner). This allows a platform to send any email to this user. The user can revoke this access at any time.



In summary:

* The user protects his email using the DataProtector
* The user grants access to his email to a platform
* The user sets his notification preferences in his TalentLayer metadata

### 2.1 Use Cases

For now, TalentLayer has outlined seven distinct use cases where email notifications can be sent to keep users informed and engaged.

{% hint style="info" %}
Each come with a default value used automatically after the user grant access.
{% endhint %}

#### 1. **Active on New Service (`activeOnNewService`)**

* **Description**: When a new gig that matches the user skills becomes available, he will be notified via email.
* **Purpose**: Ensures the user do not miss out on new opportunities that align with his skillset.
* **Default value:** false

#### 2. **Active on New Proposal (`activeOnNewProposal`)**

* **Description**: Receive an email notification whenever a new proposal is posted on a hirer Gig.
* **Purpose**: Keeps the hirer updated on the interest and activity on his posted Gigs.
* **Default value:** true

#### 3. **Active on Proposal Validated (`activeOnProposalValidated`)**

* **Description**: Be informed via email when the worker proposal has been validated.
* **Purpose**: Lets the worker know the status of his proposal, allowing him to take the next steps.
* **Default value:** true

#### 4. **Active on Fund Release (`activeOnFundRelease`)**

* **Description**: Get an email alert when the worker receive new funds from one of his job, or when the hirer get funds reimbursed
* **Purpose**: Keeps users finances in check by notifying the user of fund releases.
* **Default value:** true

#### 5. **Active on Review (`activeOnReview`)**

* **Description**: An email will be sent when the worker or the hirer receive a new review.
* **Purpose**: Helps the user monitor feedback
* **Default value:** true

#### 6. **Active on Platform Marketing (`activeOnPlatformMarketing`)**

* **Description**: Receive email notifications about important announcements, new features, and partnerships from the platform
* **Purpose**: Ensures the user is up-to-date with the latest developments and features in the platform.
* **Default value:** false

#### 7. **Active on Protocol Marketing (`activeOnProtocolMarketing`)**

* **Description**: Receive email notifications about important announcements, new features, and partnerships from the protocol
* **Purpose**: Ensures the user is up-to-date with the latest developments and features in the protocol.
* **Default value:** false



***

## 3. Iexec Tools within TalentLayer

Iexec uses two different tools in order to enable web3 mails: the **DataProtector** & the **Web3Mail**. The DataProtector module will enable a user to protect his email, grant access to his email to different addresses, fetch the data which was granted to a platform etc. The Web3Mail module is build on top of DataProtector and come with two functions. The first one fetch contacts used to get easily all the contact of a platform and the second one sendEmail use to send an email to one user by address.



### 3.1 Architecture

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Web3mail architecture - New Service notification example</p></figcaption></figure>

#### Backend:

* **Responsibilities**: Each platform within TalentLayer is entrusted with sending its own emails to its users. This approach sustains the efficient functioning of our multi-platform system.
* **Challenge Addressed**: It resolves the identified issue of architecting web3 email within TalentLayer while preserving interoperability between two platforms. For instance, a hirer on Platform A, who allows emails from Platform A, will successfully receive an email notification when a worker from Platform B makes a proposal.
* **How does it work?**
  * A cron based run one script one particular type of email. It uses TalentLayer subgraph data to get the new events that happened on the network
  * Every time something new is dedicated, it check if the platform can send him an email, and if it's the case send the email.
  * An additional database is used here to manage the issue of duplicates and down time of cron.

#### Frontend:

* **Responsibilities**: The frontend is responsible for retrieving user authorization, ensuring only permitted communications reach the users.
* **How does it works?**
  * The user is invited after important action like creating a profile or creating a service to setup email notification.&#x20;
  * The user is redirect to a dedicated page where he can first protect his email data and the authorize the current platform to access it.&#x20;
  * Last step for the user is to validate his preferences



<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption><p>User opting for web3 notifications workflow</p></figcaption></figure>

#### Admin:

* **Responsibilities**: Provides API and pages allowing owners to send emails directly, offering more control and efficiency in communication.
* **How does it works?**
  * The platform owner got access to new admin pages where he can send directly to selected pooled of user from his contact an marketing email.
  * The formular is connected with a backend API which handle the connection with iExec web3mail from the dedicated private key of the platform
  * Security note: the public/private key pair used for sending email is different from the one that manage the TalentLayer platform.

#### Graph:

* **Responsibilities**: Manages the storage of preferences, ensuring each user’s choices are honored in the email communication process.
* **How does it works?**
  * Each user got a TalentLayerId store on chain
  * Each TalentLayerId is linked to an offchain metadata in json stored on IPFS which contains all the extra information about a user.&#x20;
  * Our graph indexed these data to make it easly accessible for anyone from the API
  * Since different types of notifications are available, it's important that the user can decide for which ones he would be interested. These preferences are set it the User's metadata, in the "UserWeb3mailPreferences" entity, located in the "UserDescription":

```graphql
 type UserDescription @entity(immutable: true) { 
    id: ID! #cid 
    title: String
    about: String
    skills_raw: String
    skills: [Keyword!]
    timezone: BigInt
    headline: String
    country: String
    user: User!
    role: String # buyer, seller, both 
    name: String # Custom user name 
    video_url: String #url 
    image_url: String #url 
    web3mailPreferences: UserWeb3mailPreferences
}
```

```graphql
type UserWeb3mailPreferences @entity(immutable: true) {
    id: ID! #cid 
    activeOnNewService: Boolean 
    activeOnNewProposal: Boolean 
    activeOnProposalValidated: Boolean
    activeOnFundRelease: Boolean
    activeOnReview: Boolean
    activeOnPlatformMarketing: Boolean
    activeOnProtocolMarketing: Boolean 
}
```



####

{% hint style="info" %}
#### Bellecour sidechain is currently being used in the starterkit dedicated branch as web3mail is only working here
{% endhint %}



**Environment Variables**

There are a set of environment variables dedicated to wbe3mail which should be configured before use:

```xml
// Set to true if you with to enable web3Mail notifications
NEXT_PUBLIC_ACTIVE_WEB3MAIL=false

// Set here the Private & Public key of the ETH address which will be used to perform
// web3mails operations & signatures
NEXT_PRIVATE_WEB3MAIL_PLATFORM_PRIVATE_KEY="xaddyouprivatekeyhere"
NEXT_PUBLIC_WEB3MAIL_PLATFORM_PUBLIC_KEY="0x27FDabe8222d7f874406F3EaBBb9601D87EF1a82"

// Iexec web3mail app address
NEXT_PUBLIC_WEB3MAIL_APP_ADDRESS="web3mail.apps.iexec.eth"

// Set here the cron security key of your choice
CRON_SECRET="xxx"
```



### 3.2 DataProtector

Within TalentLayer, DataProtector functions as the backbone for secure email communication, safeguarding users’ email data with utmost integrity. It enables TalentLayer to utilize user data for personalized email notifications without exposing the actual data. By employing end-to-end encryption and confidential computing technology, DataProtector ensures that while TalentLayer can effectively use the data for email communication, the actual user data remains invisible and inaccessible, thereby upholding user privacy and data security seamlessly.

{% embed url="https://tools.docs.iex.ec/tools/dataprotector" %}

It can be used as such:

```typescript
/**
 * @dev: Generate DataProtector
 */
const PRIVATE_KEY = "set-your-private-key";
const protectorWebProvider = getProtectorProvider(PRIVATE_KEY);
const dataProtector = new IExecDataProtector(protectorWebProvider);

/**
 * @dev: Used to protect the user's email
 * @param: name: string - The name of the protected data, in our case "TalentLayer email" 
 * but it should be set to your platform's name in order to be able to filter on it later
 * @param: email: string
 */
const protectedEmail = await dataProtector.protectData({
  name: 'TalentLayer email',
  data: {
    email: 'myEmail@talentLayer.com',
  },
});
```

This method returns a `ProtectedDataWithSecretProps` object, which has an ETH address. Then the user can grant access to his email to a platform using the following method:

```typescript
/**
 * @dev: Used to grant access to a platform to the user's email
 * @param: protectedData: string - The protected email's ETH address
 * @param: userAddress: string - The ETH address of the user which protected his email
 * @param: authorizedUser: string - The ETH address of the user which will be sending emails (Platform owner)
 */
  //Iexec web3mail app address
    const NEXT_PUBLIC_WEB3MAIL_APP_ADDRESS = 'web3mail.apps.iexec.eth'

    // protected email's ETH address
    const protectedData: ProtectedData[] = await dataProtector.fetchProtectedData({
      owner: userAddress,
      requiredSchema: {
        email: 'string',
      },
    });
    
    const protectedEmail = protectedData.find(item => item.name === 'TalentLayer email');

    const grantAccessArgs: GrantAccessParams = {
      protectedData: protectedEmail,
      authorizedApp: NEXT_PUBLIC_WEB3MAIL_APP_ADDRESS,
      authorizedUser: '0x....',
    };

    await dataProtector.grantAccess(grantAccessArgs);
```

In order to check whether access was granted to a platform for a protectedData item, the following method can be used:

```typescript
/**
 * @dev: Used to fetch the list of granted access to a protectedData item
 * @param: protectedData: string - The address of the protected data (protected email in our case)
 * @return: listGrantedAccess: GrantedAccess[] - The list of granted access
 */
  const listGrantedAccess = await dataProtector.fetchGrantedAccess({
    protectedData: protectedData.address,
    authorizedApp: process.env.NEXT_PUBLIC_WEB3MAIL_APP_ADDRESS,
  });
```

After this step, the user's email is protected and access was granted to a platform, which can now send him emails using the Web3Mail provider.

***

### 3.3 Web3Mail

In TalentLayer, Web3Mail operates in conjunction with DataProtector, enhancing the security and efficiency of email communication. It mainly functions to send emails to individual users, ensuring each communication is securely delivered. Web3Mail retrieves encrypted email addresses (contacts) for which access has been granted and sends emails to those addresses

{% embed url="https://tools.docs.iex.ec/tools/web3mail" %}

It can be used as such:

```typescript
const PRIVATE_KEY = "set-your-private-key";

const mailWeb3Provider = getMailProvider(privateKey);
const web3mail = new IExecWeb3mail(mailWeb3Provider);

/**
 * @dev: Used to fetch contacts which granted access to their encrypted email to a platform
 */
const contactList: Contact[] = await web3mail.fetchMyContacts();
```

After fetching the contacts, a platform can send emails to them using the following method on each contact:

```typescript
/**
 * @dev: Used to send an email to a contact
 * @param: contactList: Contact[] - The list of contacts
 * @param: emailSubject: string - The subject of the email
 * @param: emailContent: string - The content of the email
 */
for (const contact of contactList) {
  await web3mail.sendEmail({
    protectedData: contact.address,
    emailSubject: emailSubject,
    emailContent: emailContent,
  });
}
```

For sending emails to only a set of addresses, it's important to check whether the provided address had granted access to his email to the platform. Otherwise, the sendEmail function will crash. This can be done using the DataProtector provider, by first fetching the addresses' protected data, then checking whether access was granted to the platform.

This can be done using the following method:

```typescript
/**
 * @dev: Fetch all data a user protected
 */
  const protectedData = await dataProtector.fetchProtectedData({
    owner: userAddress,
    requiredSchema: {
      email: 'string',
    },
  });

/**
 * @dev: Filter on the protected email for TalentLayer
 */
const protectedEmail = protectedData.find(item => item.name === 'TalentLayer email');

/**
 * @dev: Check whether access was granted
 */
if (protectedEmail) {
  const listGrantedAccess = await dataProtector.fetchGrantedAccess({
    protectedData: protectedEmail.address,
    authorizedApp: process.env.NEXT_PUBLIC_WEB3MAIL_APP_ADDRESS,
  });
}
```

If no access was granted, "listGrantedAccess.length" will = 0.

***

## 4. Integration in TalentLayer StarterKit

In order to enable web3mail sending within the TalentLayer ecosystem,&#x20;

### 4.1 FrontEnd - User authorization

//TODO

\=> Protecting email & Granting Access => Setting Notification preferences in Metadata

### 4.2 Backend - Notification sending

There are two kinds of notifications, punctual ones such as "Platform Marketing campaigns", which should be sent when required by a platform's owner; and regular automatic ones, such as "New Services listed matching my skills", which should be triggered by smart contract events. The Starter Kit provides an example of backend to handle these notifications using one API endpoint per Notification type. The automatic endpoints will be handled by a cron.

####

#### _Punctual_:

Notifications campaigns which will be sent on a non-programmed manner will be sent using the "sendEmail" function of the Web3Mail provider. The only checks to be done is whether the user granted access to his email to the platform & whether the user opted for this feature.



<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>Platform Marketing Notification workflow</p></figcaption></figure>



The StarterKit provides an API example to send Platform marketing notifications:

_Platform Marketing Campaigns_

```
@params: 
    emailSubject: string, 
    emailContent: string,
    signature: string,
    throwable? :boolean
    
/api/web3mail/platform-marketing
```

In order to secure this API endpoint and make sure that only the platform owner can call it, a signature is required upon sending emails, and sent as a param in the body of the http request.



{% hint style="info" %}
The message signed for this security check is the subject of the email
{% endhint %}



The API will first check whether the signature in the body of the request was sent by the ETH address of the platform owner.



In summary:

1 - Fetch all contacts using web3mail provider

2 - Check which of these contacts opted for this feature using a graph call to TalenyLayer graph to check user's metadata

3 - Provide signature to the API call

4 - Send the email to all Users checking these 2 conditions

####

#### _Automatic_:

The automatic notifications will require a script to regularly fetch data from the TalentLayer graph in order to check whether the watched event has occured. If we want to notify users when a new proposal was made for his service, we will need to regularly fetch the list of proposals for each service, and check whether a new one was made (checking this against the "updatedAt" graph field). If so, we will need to send an email to the service's owner.

In the StarterKit, the automatic notifications are handled by a cron, which will regularly fetch the data from the graph, and send the notifications if required. The used cron is the integrated Vercel cron system, but you can use any system you prefer.



<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Vercel Cron Notification workflow for "New Proposal" notification</p></figcaption></figure>



_**Example of a cron job: New Payment Notification**_

In order to illustrate the workflow of an automatic notification, we will take the example of the "New Payment" notification, which will be sent when a payment is made for a service.

The notification will be sent using an API endpoint, which will be called by the cron job. In order for this Endpoint to be ONLY callable by the cron, a cron key will be set in the .env file, and the cron will have to provide this key as a request param to be authorized to call the API. This way, the endpoint will only be callable by the cron.

1 - **Setting the cron Pattern**

Cron patterns are set in the vercel.json file at the root of the project.



Each API endpoint is associated with an API endpoint which will be called by the cron. We want to check for new notifications every hour, so we need to set a cron pattern for the "fund-release" endpoint, which will be called every hour.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

2 - **Secure API Endpoint with a key**

Each of these endpoints are secured by a secret key to ensure that only the cron can call them. If you set an environment variable called CRON\_SECRET="xxx", then Vercel will add this in the Authorization headers of each API called by the cron.

Each cron API call begins by a series of checks found in the "_prepareCronApi()_" function, one of them being a comparison between this header value and your environment variable. This way you can freely develop an open source project while keeping your your routes secure.

{% hint style="warning" %}
So remember to set the CRON\_SECRET environment variable prior to deployment.
{% endhint %}



3 - **Fetching Data from the Graph**

After this first check, the list of payments executed within the last hour will be fetched from the TL Graph:

```
{
payments(
orderBy: createdAt
where: {service_: {platform: "${id}"} , createdAt_gt: "${timestamp}"}
) {
    id
    amount
    createdAt
    paymentType
    ...
    }
}
```

The "createdAt\_gt" graph param will be used for this check. The "timestamp" variable will be set to the last cron execution minus one hour.



4 - **Integrating a retry factor**

With this system, if an email does not get sent for any technical reason, it will not be sent again. Therefore, we decided to integrate a **retry factor**, which will multiply the cron duration by the retry factor, so that the graph query will fetch data further in time. With a retry factor of 3, the cron will fetch data for the last 3 hours, and send the email if a payment was made during this period. This way, if an email was not sent, there will be 3 attempts.



5 - **Recording sent notifications in a database**

In case a retry factor was set and in order to avoid sending the same notification twice, we decided to record the sent notifications in a database. This way, each time the cron runs it can check in the database whether a detected notification was already sent, and avoid sending it again. In the Starter Kit we provide a solution using MongoDB, and persist sent notifications as such:

```typescript
/**
 * @dev: Web3MailNotification MongoDD schema
 * @param: id: string - The unique id of the notification
 * @param: sentAt: number - The timestamp at which the notification was sent
 * @param: type: EmailType enum - The type of the notification
 */
const web3MailSchema = new Schema({
  id: {
    type: String,
    required: true,
    unique: true,
  },
  sentAt: {
    type: Number,
    required: true,
    unique: false,
  },
  type: {
    type: String,
    enum: EmailType,
    required: true,
  },
});
```

For the "New Payment" notification, after each sent email, an entity will be recorded with its id following this format: `<"paymentId"-"EmailType.fundRelease">` This way unicity is granted.

#### Summary: Automatic notification workflow

Now all is technically ready for a cron to send the notification. The workflow is the following:

* Check all required API data (summed up in the "prepareCronApi()" function)
* Connect to the database
* Calculate cron duration & last execution timestamp
* Fetch new payments data from the graph
* Check whether a notification was already sent for each payment
* If notifications need to be sent, check whether the user opted for this feature in his metadata
* If yes, check whether the user granted access to his email to the platform
* If yes, send the notification using the Web3Mail provider
* If email was sent, record it in the database

#### List of available notifications & API endpoints

The available punctual notification is:

**Platform Marketing**

_Notification punctually sent by platforms for marketing purposes_

```
/api/web3mail/platform-marketing
```



The list of available automatic notifications & associated API endpoints are:

New Service

_Sent to users when a new service matching at least one of their skills was published_

```
/api/web3mail/new-service
```

Fund Release

_Sent to a seller when a fund release has be sent to his account, or to the buyer if a reimbursement has been sent to his account._

```
/api/web3mail/fund-release
```

Proposal Validated

_Sent to a seller when one of their proposals has been validated_

```
/api/web3mail/proposal-validated
```

New Proposal

_Sent to a buyer when a new proposal has been made for one of their services_

```
/api/web3mail/new-proposal
```

New Review

_Sent to users when they receive a review_

```
/api/web3mail/review
```
