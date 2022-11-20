# Metadata

## On-Chain Metadata

### TalentLayer ID Metadata

```json
 //Emit when new TalentLayerID is minted.
 //@param _user Address of the owner of the TalentLayerID
 //@param _tokenId TalentLayer ID for the user
 //@param _handle Handle for the user
 //@param _withPoh Whether a user has a POH 
{
    "user": ""
    "withPoh": "",
    "tokenId": "",
    "handle": "",
}
```

### Service Metadata

```json
/// @notice Service information struct
/// @param status the current status of a service
/// @param employerId the talentLayerId of the employer
/// @param employeeId the talentLayerId of the employee
/// @param initiatorId the talentLayerId of the user who initialized the service
/// @param serviceDataUri token Id to IPFS URI mapping
{  
   "employerId": "",
   "employeeId": "",
   "initiatorId": "",
   "serviceDataUri": ""
 }
```

### Review Metadata

```json
/// @param serviceId the id of the service that is being reviewed
/// @param toId the id of the person the review is for (recipient)
/// @param tokenID the token id of the review NFT
/// @param token token Id to IPFS URI mapping
{
    "serviceId": "",
    "toId": "",
    "tokenId": "",
    "reviewUri": ""
}
```

## Metadata on IPFS

### Service Metadata

```json
//Unfilled Service Metadata
{
    "service_title": "",
    "service_about": "",
    "service_keywords": ["", "", ""]
}

//Example Service Metadata
{
    "service_title": "Bug Fix for Gitbook",
    "service_about": "Our tool does not size rows and columns properly. We will be hiring @rickroll for a short-term $25/hour role payable in USDT. Expected completion of the bug fix is July 30th.",
    "service_keywords": ["ui/ux", "bug", "developer"]
}
```

### Review Metadata

```json
//Unfilled Review Metadata
{
    "role": "",
    "rating": "",
    "service_review": ""
}

//Example Review Metadata
{
    "role": "hirer",
    "rating": "5",
    "service_review": "They did a great job. Will be hiring them again in the future. Prompt communication and timeley delivery."
}
```
