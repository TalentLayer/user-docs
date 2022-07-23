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

### Job Metadata

```json
/// @notice Job information struct
/// @param status the current status of a job
/// @param employerId the talentLayerId of the employer
/// @param employeeId the talentLayerId of the employee
/// @param initiatorId the talentLayerId of the user who initialized the job
/// @param jobDataUri token Id to IPFS URI mapping
{  
   "employerId": "",
   "employeeId": "",
   "initiatorId": "",
   "jobDataUri": ""
 }
```

### Review Metadata

```json
/// @param jobId the id of the job that is being reviewed
/// @param toId the id of the person the review is for (recipient)
/// @param tokenID the token id of the review NFT
/// @param token token Id to IPFS URI mapping
{
    "jobId": "",
    "toId": "",
    "tokenId": "",
    "reviewUri": ""
}
```

## Metadata on IPFS

### Job Metadata

```json
//Unfilled Job Metadata
{
    "job_title": "",
    "job_about": "",
    "job_keywords": ["", "", ""]
}

//Example Job Metadata
{
    "job_title": "Bug Fix for Gitbook",
    "job_about": "Our tool does not size rows and columns properly. We will be hiring @rickroll for a short-term $25/hour role payable in USDT. Expected completion of the bug fix is July 30th.",
    "job_keywords": ["ui/ux", "bug", "developer"]
}
```

### Review Metadata

```json
//Unfilled Review Metadata
{
    "role": "",
    "transaction": "",
    "rating": "",
    "job_review": ""
}

//Example Review Metadata
{
    "role": "hirer",
    "transaction": "0xe452ac682d80793a354ed2b89efe30ba70b30a0205919740395e8ee5685c1f6d",
    "rating": "5",
    "job_review": "They did a great job. Will be hiring them again in the future. Prompt communication and timeley delivery."
}
```
