# Metadata

{% hint style="info" %}
**What Metadata Is Required?** On-chain metadata is required operationally for TalentLayer. Off-chain metadata is a mixture of required and optional. Please refer to each data element for the specifics. For optional metadata, you can choose to allow users to submit information for the fields or you can choose to disregard the data fields.
{% endhint %}

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
title // 
about // user's about me information
skills // user's skill keywords
timeZone // OPTIONAL 
headline // OPTIONAL 
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
names 
takenNames
platformUri // Link to the off-chain (IPFS) data
fee // Fee configured for Platform Fee
```

</details>

<details>

<summary>PlatformID IPFS</summary>

```json
about
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
countProposals 
transactionId 
platformId // Platform ID of the platform who facilitated post of service
```

</details>

<details>

<summary>Service IPFS</summary>

```json
title
about
startDate // start date of work, if applicable
expectedEndDate // end date of work, if applicable
keywords 
role // is the service posted by a seller or a buyer
rateToken // the token that the payment will be made in (token address mapped to a ticker sign)
rateAmount // number of tokens to be paid
recipient // TalentLayer ID of the seller/worker
location // OPTIONAL
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
startDate
title
about
expectedHours // OPTIONAL
```

</details>

{% content-ref url="smart-contracts/serviceregistry.sol.md" %}
[serviceregistry.sol.md](smart-contracts/serviceregistry.sol.md)
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
PaymentType 
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
Arbitrable
Choices
fee
ruling
DisputeStatus (Waiting, Appealable, Solved)
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
rating 
```

</details>

{% content-ref url="smart-contracts/talentlayerreview.sol.md" %}
[talentlayerreview.sol.md](smart-contracts/talentlayerreview.sol.md)
{% endcontent-ref %}

{% hint style="info" %}
**Numeric Rating:** We intend to eventually remove the numeric rating metadata piece in the review element. Numeric ratings are highly subjective across diverse platforms and it is better if these ratings are calculated by the platforms themselves.
{% endhint %}
