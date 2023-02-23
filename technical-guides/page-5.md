# Metadata

In this section we provide all metadata elements that are used as a part of TalentLayer today. Included below are comments explaining each piece of metadata and giving information on requirements of the various data pieces.&#x20;

{% hint style="info" %}
**Think We're Missing Something?** We're taking active feedback on our metadata and would love to hear what you think about our data structures. Have an opinion? Reach out to our team via the "Get Help" page of these docs.&#x20;
{% endhint %}

## **What Metadata Is Required For My Platform To Use?**&#x20;

All on-chain metadata (except for metadata relating to third-party on-chain integrations) is required operationally for TalentLayer. These required metadata elements are necessary for your platform to function using TalentLayer.

Off-chain metadata is a mixture of required, optional, and recommended. Please refer to each data element for the specifics.&#x20;

Optional metadata is labeled "OPTIONAL"

Recommended metadata is labeled "RECOMMENDED"&#x20;

All other metadata elements not labeled can be considered required.

For optional and recommended metadata, you can choose to allow users to submit information for the fields or you can choose to disregard the data fields.&#x20;

Recommended metadata improves search-ability and user experience, but will still allow your workflows to function if left out.&#x20;

## TalentLayer ID

<details>

<summary>TalentLayerID On-Chain</summary>

```json
id // nft identifier 
handle // user's TalentLayer ID handle
pohAddress // OPTIONAL user's proof of humanity address
PlatformId // the platform where an ID was minted from
DataUri (CID) // Link to the off-chain (IPFS) data
```

</details>

<details>

<summary>TalentLayerID IPFS</summary>

```json
title // RECOMMENDED a user's professional title (e.g. "developer", "creative marketing expert")
about // RECOMMENDED user's about me information
skills // RECOMMENDED user's skill keywords
timeZone // OPTIONAL 
headline // OPTIONAL an introduction headline (e.g. "passionate developer looking for solidity opportunities")
country // OPTIONAL
picture // OPTIONAL
```

</details>

{% content-ref url="smart-contracts/talentlayerid.sol.md" %}
[talentlayerid.sol.md](smart-contracts/talentlayerid.sol.md)
{% endcontent-ref %}

## Platform ID

<details>

<summary>PlatformID On-Chain</summary>

```json
id // nft identifier 
name // platform's ID handle - usually name of platform
platformUri // Link to the off-chain (IPFS) data
fee // Fee configured for Platform Fee
```

</details>

<details>

<summary>PlatformID IPFS</summary>

```json
about // OPTIONAL
website // OPTIONAL
country // OPTIONAL
logo // OPTIONAL
```

</details>

{% hint style="warning" %}
**Update In Progress:** To support Platform Managed Arbitration, we will be updating our Platform ID metadata in mid-December 2022.
{% endhint %}

{% content-ref url="smart-contracts/talentlayerplatformid.sol.md" %}
[talentlayerplatformid.sol.md](smart-contracts/talentlayerplatformid.sol.md)
{% endcontent-ref %}

## Service & Proposal

### Service

<details>

<summary>Service On-Chain</summary>

```json
Status: Opened / Confirmed / Finished / Rejected 
buyerId // TalentLayer ID handle of the buyer/hirer
sellerId // TalentLayer ID handle of the seller/worker
initiatorId // TalentLayer ID handle of the user who initiated the work 
serviceDataUri // Link to the off-chain (IPFS) data
countProposals // The total number of proposal for this service
transactionId // the escrow transaction ID linked to the service
platformId // Platform ID of the platform who facilitated post of service
```

</details>

<details>

<summary>Service IPFS</summary>

```json
title // title of the job
about // about the job
startDate // RECOMMENDED start date of work, if applicable
expectedEndDate // RECOMMENDED end date of work, if applicable
keywords // RECOMMENDED keywords of the job
role // is the service posted by a seller or a buyer
rateToken // the token that the payment will be made in (token address mapped to a ticker sign)
rateAmount // number of tokens to be paid
recipient // TalentLayer ID of the seller/worker
location // OPTIONAL Location of user
```

</details>

### Proposal

<details>

<summary>Proposal On-Chain</summary>

```json
Status ; Pending / Validated / Rejected
sellerId // Talentlayer ID of the seller/worker
rateToken // the token that the payment is requested in (token address mapped to a ticker sign)
rateAmount // Numeber of tokens requested
proposalDataUri // Link to the off-chain (IPFS) data
```

</details>

<details>

<summary>Proposal IPFS</summary>

```json
startDate // RECOMMENDED start date of work for proposal
title // title of proposal
about // details of the proposal
expectedHours // OPTIONAL
```

</details>

{% content-ref url="smart-contracts/talentlayerservice.sol.md" %}
[talentlayerservice.sol.md](smart-contracts/talentlayerservice.sol.md)
{% endcontent-ref %}

## Escrow

### Transaction

<details>

<summary>Escrow Transaction On-Chain</summary>

```json
sender // person who sends funds (buyer)
receiver // person who recived funds (seller)
token // the token that is in the escrow contract
amount // the number of tokens in the escrow contract
serviceId // the identifier for the service the escrow is related to
```

</details>

### Payment

<details>

<summary>Escrow Payment On-Chain</summary>

```json
paymentType // can be either “release” (pay the seller) or “reimburse” (money back to the buyer)
token // the token that is in the escrow contract
amount // the number of tokens in the escrow contract
serviceId // the identifier for the service the escrow is related to
```

</details>

{% content-ref url="smart-contracts/escrow-and-dispute.md" %}
[escrow-and-dispute.md](smart-contracts/escrow-and-dispute.md)
{% endcontent-ref %}

## Arbitrator

<details>

<summary>Kleros Arbitrator On-Chain</summary>

```json
Arbitrable // contract that the arbitatror is ruling on (where the dispute came from, e.g. our escrow)
Choices // number of different choices that the arbitrator can make (the number of possible outcomes of the dispute)
fee // arbitration fee, amount that must be paid to the arbitrator in order to raise a dispute
ruling // decision taken by the arbitrator (must be one of the available choices or 0, which stands for “refused to arbitrate”)
DisputeStatus (Waiting, Appealable, Solved) // current status of the dispute - whether it has just been created, or a ruling has been given but can still be appealed, or is definitely solved
```

</details>

{% content-ref url="smart-contracts/escrow-and-dispute.md" %}
[escrow-and-dispute.md](smart-contracts/escrow-and-dispute.md)
{% endcontent-ref %}

{% hint style="warning" %}
**Update In Progress:** To support Platform Managed Arbitration, we will be updating our Arbitrator metadata in mid-December 2022.
{% endhint %}

## Review

<details>

<summary>Review On-Chain</summary>

```json
serviceId // the identifier for the service the escrow is related to
toId // the TalentLayer ID of the receiver of the review
tokenId // identifier for the review NFT
rating 
reviewUri // Link to the off-chain (IPFS) data
platformId // the platform where an ID was minted from
```

</details>

<details>

<summary>Review IPFS</summary>

```json
content // text content of the review 
rating // OPTIONAL 1-5 star rating for the work done
```

</details>

{% content-ref url="smart-contracts/talentlayerreview.sol.md" %}
[talentlayerreview.sol.md](smart-contracts/talentlayerreview.sol.md)
{% endcontent-ref %}

{% hint style="info" %}
**Numeric Rating:** We intend to eventually remove the numeric rating metadata piece in the review element. Numeric ratings are highly subjective across diverse platforms and it is better if these ratings are calculated by the platforms themselves.
{% endhint %}
