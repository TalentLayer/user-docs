# Metadata

{% hint style="info" %}
**What Metadata Is Required?** On-chain metadata is required operationally for TalentLayer. Off-chain metadata is a mixture of required and optional. Please refer to each data element for the specifics. For optional metadata, you can choose to allow users to submit information for the fields or you can choose to disregard the data fields.
{% endhint %}

## TalentLayer ID

<details>

<summary>TalentLayerID On-Chain</summary>

```json
id
handle
pohAddress
PlatformId
DataUri (CID)
```

</details>

<details>

<summary>TalentLayerID IPFS</summary>

```json
title
about
skills 
timeZone //Optional
headline //Optional
country //Optional
picture //Optional
```

</details>

{% content-ref url="smart-contracts/talentlayerid.sol.md" %}
[talentlayerid.sol.md](smart-contracts/talentlayerid.sol.md)
{% endcontent-ref %}

## Platform ID

<details>

<summary>PlatformID On-Chain</summary>

```json
id
names
takenNames
platformUri
fee
```

</details>

<details>

<summary>PlatformID IPFS</summary>

```json
about
website //Optional
country //Optional
logo //Optional
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
Status : Opened / Confirmed / Finished / Rejected
buyerId
sellerId
initiatorId
serviceDataUri
countProposals
transactionId
platformId
```

</details>

<details>

<summary>Service IPFS</summary>

```json
title
about
startDate
expectedEndDate
keywords
role
rateToken
rateAmount
recipient
location //Optional
```

</details>

### Proposal

<details>

<summary>Proposal On-Chain</summary>

```json
Status ; Pending / Validated / Rejected
sellerId
rateToken
rateAmount
proposalDataUri
```

</details>

<details>

<summary>Proposal IPFS</summary>

```json
startDate
title
about
expectedHours
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
sender
receiver
token
amount
serviceId
```

</details>

### Payment

<details>

<summary>Escrow Payment On-Chain</summary>

```json
PaymentType
amount
token
serviceId
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
serviceId
toId
tokenId
rating
reviewUri
platformId
```

</details>

<details>

<summary>Review IPFS</summary>

```json
content
rating
```

</details>

{% content-ref url="smart-contracts/talentlayerreview.sol.md" %}
[talentlayerreview.sol.md](smart-contracts/talentlayerreview.sol.md)
{% endcontent-ref %}

