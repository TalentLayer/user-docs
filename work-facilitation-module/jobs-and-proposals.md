# Jobs & Proposals

The TalentLayer Universal Work Facilitation Module is a searchable on-chain repository of jobs/bounties that can be posted to and read from by any integrated platform. This cross-posting allows for a broader range of users to view and submit proposals for jobs.&#x20;

The Universal Work Facilitation contains a few sub-components that can be used together or separately based on the goals of your platform.&#x20;

## Jobs

Jobs are created by Users on TalentLayer-integrated platforms or by users directly by interfacing with the TalentLayer smart contracts. Job metadata is stored in the JobRegistry.sol smart contract and on IPFS.&#x20;

Jobs are viewed on platforms by searching the TalentLayer Graph based on keywords, geographic origins, job types, and other factors.&#x20;

### Job Statuses

Jobs are assigned different statuses based on the stage of the job lifecycle they are in.&#x20;

```
    enum Status {
        Filled, /// The job has been assigned to an employee
        Confirmed, /// The job has been consented to by an employee
        Finished, /// (if no escrow) The job has been market completed by an employer or (if escrow) escrow has been released 
        Rejected, /// The job has been removed by the employer
        Opened /// The job has been created, but not assigned to an employee
    }
```

## Proposals

The TalentLayer Jobs Module can be implemented with or without proposals.

Both Jobs with Proposals and Jobs without Proposals are both executable across multiple platforms, as long as they are connected with the [TalentLayer Escrow System.](escrow-and-dispute-system.md)&#x20;

For example, User A, the employer can post a Job on Platform Y and User B can search for and submit a Proposal for that Job on Platform Z.

When a proposal is created by a user for a job, the proposal is stored in an array inside the metadata of the job.&#x20;

Up to 40 proposals can be active at one time for a job. An employer can reject proposals they do not want, thus allowing new proposals to be submitted.&#x20;

### Jobs Without Proposals

Platforms may want to implement a workflow where users can create jobs without proposals if they want their users to be able to directly assign employees for a job, without receiving open proposals.&#x20;

In this implementation, the employer defines factors like pay rate and terms, with no on-chain counter-proposals possible from the potential employee's end.&#x20;

### Jobs With Proposals

Platforms may want to implement a workflow where users can create jobs with proposals if they want users to be able to post jobs and have potential employees submit proposals for those jobs.&#x20;

In this implementation, the Proposal defines the final pay rate and terms. When the Proposal is accepted by the employer, those terms are accepted.&#x20;
