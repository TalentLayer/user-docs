---
description: >-
  Here we will see how a buyer can validate a proposal with the
  createTransaction function.
---

# How to implement the proposal validation?

## Good to Know

In this example, we will use reactJS, Ether.js and formik to handle the form on the frontend. You will find a full code example with all imports at the end of tutorial.&#x20;

## ① The proposal validation process

To validate a proposal the buyer have to send the validated amount to the escrow contract, in our Dapp, this step happen by clicking on the validate proposal button in the `ValidateProposalModal` component.

But let's see how the process is organized

**1 - `ServiceDetail` component :** you will have in this component the mapping of all proposal, it use the `ProposalItem` component.

```tsx
<div className='grid grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-4'>
  {validatedProposal ? (
    <ProposalItem proposal={validatedProposal} />
  ) : (
    proposals.map((proposal, i) => {
      return (
        <div key={i}>
          {(service.status === ServiceStatusEnum.Opened ||
            proposal.status === ProposalStatusEnum.Validated) && (
            <ProposalItem proposal={proposal} />
          )}
        </div>
      );
    })
  )}
</div>
```

**2-`ProposalItem`** component : this component will display all the proposal details and it use the `ValidateProposalModal`

```tsx
<div className='flex flex-row gap-4 justify-between items-center border-t border-gray-100 pt-4'>
  <p className='text-gray-900 font-bold line-clamp-1 flex-1'>
    {renderTokenAmount(proposal.rateToken, proposal.rateAmount)}
  </p>
  {account && isBuyer && proposal.status === ProposalStatusEnum.Pending && (
    <ValidateProposalModal proposal={proposal} account={account} />
  )}
</div>
```

**3-`ValidateProposalModal`**component : this component will display a modal with all the information of the proposal, including the fee's summary, total, account balance

* **Validate proposal** button : on submit, it will call ValidateProposal function

```tsx
const onSubmit = async () => {
    if (!signer || !provider) {
      return;
    }
    await validateProposal(
      signer,
      provider,
      proposal.service.id,
      proposal.seller.id,
      proposal.rateToken.address,
      proposal.cid,
      totalAmount,
    );
    setShow(false);
  };
```

* **Decline** button : used to decline a proposal
* **Contact the seller** button : used to contact and chat with the seller with the xmtp decentralized instant message service



Let's focus on `ValidateProposalModal` component

**4-`ValidateProposal`** component : this component is the **core** of the proposal validation process.

As you can see below it take a few parameter

```tsx
export const validateProposal = async (
  signer: Signer,
  provider: Provider,
  serviceId: string,
  proposalId: string,
  rateToken: string,
  cid: string,
  value: ethers.BigNumber,
): Promise<void> => {
  const talentLayerEscrow = new Contract(
    config.contracts.talentLayerEscrow,
    TalentLayerEscrow.abi,
    signer,
  );
```

1. `signer: Signer`: This parameter is of type `Signer` and is required. It represents the Ethereum account that will sign the transaction.
2. `provider: Provider`: This parameter is of type `Provider` and is required. It represents the Ethereum network provider that will be used to submit the transaction.
3. `serviceId: string`: This parameter is of type `string` and is required. It represents the ID of the service concerned by the proposal.
4. `proposalId: string`: This parameter is of type `string` and is required. It represents the ID of the proposal that is being validated.
5. `rateToken: string`: This parameter is of type `string` and is required. It represents the address of the ERC-20 token that is being used to pay for the service. If this is set to `ethers.constants.AddressZero`, then the payment is being made in Ether
6. `cid: string`: This parameter is of type `string` and is required. It represents the IPFS CID of the evidence that is being used to validate the proposal.
7. `value: ethers.BigNumber`: This parameter is of type `ethers.BigNumber` and is required. It represents the amount of tokens or that is being used to pay for the service.

Then you have the `createTranscation` call, the proposal will be validated as soon as the transcation is validated

\==> If the used token is ETH then the createTransaction is directly call with the right parameter

```tsx
if (rateToken === ethers.constants.AddressZero) {
  const tx1 = await talentLayerEscrow.createTransaction(
    parseInt(serviceId, 10),
    parseInt(proposalId, 10),
    metaEvidenceCid,
    cid,
    {
      value,
    },
);
```

\==> If the token is another ERC-20 token then you have have to pass trought a few more validation step as&#x20;

* Check the ERC-20 token balance

```tsx
const balance = await ERC20Token.balanceOf(signer.getAddress());
  if (balance.lt(value)) {
    throw new Error('Insufficient balance');
}
```

* Check the token allowance

```tsx
const allowance = await ERC20Token.allowance(
    signer.getAddress(),
    config.contracts.talentLayerEscrow,
  );

  if (allowance.lt(value)) {
    const tx1 = await ERC20Token.approve(config.contracts.talentLayerEscrow, value);
    const receipt1 = await toast.promise(provider.waitForTransaction(tx1.hash), {
      pending: {
        render() {
          return (
            <TransactionToast
              message='Your approval is in progress'
              transactionHash={tx1.hash}
            />
          );
        },
      },
      success: 'Transaction validated',
      error: 'An error occurred while updating your profile',
    });
    if (receipt1.status !== 1) {
      throw new Error('Approve Transaction failed');
    }
  }
```

Then we can create the new createTransaction

```tsx
const tx2 = await talentLayerEscrow.createTransaction(
    parseInt(serviceId, 10),
    parseInt(proposalId, 10),
    metaEvidenceCid,
    cid,
);
```

## See the Full Code Implemented on Our Demo DAPP

* **ServiceDetail** : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/ServiceDetail.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/ServiceDetail.tsx)
* ProposalItem : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/ProposalItem.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/ProposalItem.tsx)
* ValidateProposalModal : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Modal/ValidateProposalModal.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Modal/ValidateProposalModal.tsx)
* ValidateProposal : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/contracts/acceptProposal.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/contracts/acceptProposal.tsx)
