---
description: >-
  In this section, we will provide a detailed explanation of how the
  mintForAddress function works, which allows users to mint their TalentLayerID
  without paying any fees.
---

# How mintForAddress works

## 1 - The Front End

The workflow begins in the TalentLayerIdForm, where the user can select their handle and mint their TalentLayerID. As we have seen in the previous sections, if delegation is not activated, the workflow remains unchanged and follows the steps outlined below:

1. Select your handle.
2. Click on the mint button, triggering the onSubmit function.
3. It checks the handle price and then calls the mint function.

Now, we introduce an additional step in the workflow, specifically for delegation. As mentioned before, if delegation is activated, it triggers the `delegateMintID` function. Let's examine the code below.

```tsx
const onSubmit = async (
    submittedValues: IFormValues,
    { setSubmitting }: { setSubmitting: (isSubmitting: boolean) => void },
  ) => {
    if (account && account.address && account.isConnected && provider && signer) {
      try {
        const contract = new ethers.Contract(
          config.contracts.talentLayerId,
          TalentLayerID.abi,
          signer,
        );

        const handlePrice = await contract.getHandlePrice(submittedValues.handle);
        console.log(process.env.NEXT_PUBLIC_ACTIVE_DELEGATE_MINT);

        if (process.env.NEXT_PUBLIC_ACTIVE_DELEGATE_MINT === 'true') {
          const response = await delegateMintID(
            submittedValues.handle,
            handlePrice,
            account.address,
          );
          tx = response.data.transaction;
        } else {
          tx = await contract.mint(process.env.NEXT_PUBLIC_PLATFORM_ID, submittedValues.handle, {
            value: handlePrice,
          });
        }
        await createTalentLayerIdTransactionToast(
          {
            pending: 'Minting your Talent Layer Id...',
            success: 'Congrats! Your Talent Layer Id is minted',
            error: 'An error occurred while creating your Talent Layer Id',
          },
          provider,
          tx,
          account.address,
        );

        setSubmitting(false);
        // TODO: add a refresh function on TL context and call it here rather than hard refresh
        router.reload();
      } catch (error: any) {
        showErrorTransactionToast(error);
      }
    } else {
      openConnectModal();
    }
  };
```

The `delegateMintID` function is called only if the environment variable `process.env.NEXT_PUBLIC_ACTIVE_DELEGATE_MINT` is set to true. So, what happens in this function?&#x20;

Well, nothing new :) It first calls the appropriate API Next route, as shown below:

```typescript
export const delegateMintID = async (
  handle: string,
  handlePrice: any,
  userAddress: string,
): Promise<any> => {
  try {
    return await axios.post('/api/delegate/mint-id', {
      handle,
      handlePrice,
      userAddress,
    });
  } catch (err) {
    console.error(err);
    throw err;
  }
};
```

In the mint-id API, it follows the steps we discussed earlier by obtaining the new signer and triggering the `mintForAddress` function, which mints the TalentLayerID for the user.

```tsx
export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  const { handle, handlePrice, userAddress } = req.body;

  // @dev : you can add here all the check you need to confirm the delagation for a user

  try {
    if (process.env.NEXT_PUBLIC_ACTIVE_DELEGATE_MINT !== 'true') {
      res.status(500).json('Delegation is not activated');
      return null;
    }

    const signer = await getDelegationSigner(res);

    if (!signer) {
      return;
    }

    const talentLayerID = new Contract(config.contracts.talentLayerId, TalentLayerID.abi, signer);
    const transaction = await talentLayerID.mintForAddress(
      userAddress,
      process.env.NEXT_PUBLIC_PLATFORM_ID,
      handle,
      {
        value: handlePrice,
      },
    );

    res.status(200).json({ transaction: transaction });
  } catch (error) {
    console.log('errorDebug', error);
    res.status(500).json({ error: error });
  }
}
```

The mintForAddress contract function requires four parameters:

1. `userAddress`: This is the address of the user who wishes to mint their TalentLayerID.
2. `process.env.NEXT_PUBLIC_PLATFORM_ID`: This is the platform ID set up in the .env file.
3. `handle`: This is the selected handle chosen by the user.
4. `handleprice`: This represents the price of the handle. For the exact cost of a handle, please refer to the TalentLayer website.

## See the Full Code Implemented on Our Demo DAPP

* TalentLayerIDForm : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/TalentLayerIdForm.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/TalentLayerIdForm.tsx)
* request.ts : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/request.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/request.ts)
* mint-id API : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/api/delegate/mint-id.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/api/delegate/mint-id.ts)
* getDelegationSigner : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/api/utils/delegate.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/api/utils/delegate.ts)
