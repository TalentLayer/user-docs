---
description: >-
  In this section, we will cover in detail how delegation works for the service
  creation.
---

# Service creation example

The process is essentially the same for all the actions we have covered (except for minting delegation, which will be discussed in a separate section). Now, let's focus on delegation for service creation.

## 1 – The front end

First, we need to modify our ServiceForm.tsx component. If you recall, the classic workflow was as follows:

1. Fill out the service creation form.
2. Click on submit.
3. It triggers the onSubmit function, which calls the `createService` function in the `TalentLayerService` contract.

Now, we will add a new step that checks if delegation is activated. If it is, we will call the relevant API.

```tsx
// ..............

const { isActiveDelegate } = useContext(TalentLayerContext);

// ..............
 if (isActiveDelegate) {
    const response = await delegateCreateService(user.id, user.address, cid);
    tx = response.data.transaction;
  } else {
    const contract = new ethers.Contract(
      config.contracts.serviceRegistry,
      ServiceRegistry.abi,
      signer,
    );

    tx = await contract.createService(
      user?.id,
      process.env.NEXT_PUBLIC_PLATFORM_ID,
      cid,
      signature,
    );
  }  
```

As you can see, we check if delegation is activated using the `isActiveDelegate` variable. If it is, we call the `delegateCreateService` function. Let's take a closer look at it.

## 2 - The Back end

The `delegateCreateService` is a part of the Next API management workflow. You can explore further details in the Next [Next API documentation](https://nextjs.org/docs/pages/building-your-application/routing/api-routes)

```tsx
export const delegateCreateService = async (
  userId: string,
  userAddress: string,
  cid: string,
): Promise<any> => {
  try {
    return await axios.post('/api/delegate/create-service', {
      userId,
      userAddress,
      cid,
    });
  } catch (err) {
    console.error(err);
    throw err;
  }
}
```

In the code above, we are calling the `/api/delegate/create-service` API&#x20;

{% hint style="info" %}
You can find all the delegate API in `pages > api > delegate`
{% endhint %}

```typescript
// pages/api/createService.ts
import { NextApiRequest, NextApiResponse } from 'next';
import { Contract } from 'ethers';
import { config } from '../../../config';
import TalentLayerService from '../../../contracts/ABI/TalentLayerService.json';
import { getServiceSignature } from '../../../utils/signature';
import { getDelegationSigner, isPlatformAllowedToDelegate } from '../utils/delegate';

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  const { userId, userAddress, cid } = req.body;

  // @dev : you can add here all the check you need to confirm the delagation for a user
  await isPlatformAllowedToDelegate(userAddress, res);

  try {
    const signer = await getDelegationSigner(res);
    if (!signer) {
      return;
    }

    const signature = await getServiceSignature({ profileId: Number(userId), cid });
    const serviceRegistryContract = new Contract(
      config.contracts.serviceRegistry,
      TalentLayerService.abi,
      signer,
    );

    const transaction = await serviceRegistryContract.createService(
      userId,
      process.env.NEXT_PUBLIC_PLATFORM_ID,
      cid,
      signature,
    );

    res.status(200).json({ transaction: transaction });
  } catch (error) {
    console.log('errorDebug', error);
    res.status(500).json('tx failed');
  }
}

```

An <mark style="color:orange;">important</mark> part of the code below is that we set a new signer (the platform) for the `createService` transaction. The new signer is based on and composed of the variables you have set up in the .env file:

* `NEXT_PRIVATE_DELEGATE_SEED_PHRASE`
* `NEXT_PUBLIC_DELEGATE_ADDRESS`

```tsx
 const signer = await getDelegationSigner(res);
```

```typescript
import { NextApiResponse } from 'next';
import { ethers, Wallet } from 'ethers';
import { config } from '../../../config';
import { getUserByAddress } from '../../../queries/users';

export async function isPlatformAllowedToDelegate(
  userAddress: string,
  res: NextApiResponse,
): Promise<boolean> {
  const getUser = await getUserByAddress(userAddress);
  const delegateAddresses = getUser.data?.data?.users[0].delegates;

  if (
    delegateAddresses.indexOf(
      (process.env.NEXT_PUBLIC_DELEGATE_ADDRESS as string).toLowerCase(),
    ) === -1
  ) {
     res.status(500).json('Delegation is not activated');
    return false;
  }

  return true;
}

export async function getDelegationSigner(res: NextApiResponse): Promise<Wallet | null> {
  const provider = new ethers.providers.JsonRpcProvider(process.env.NEXT_PUBLIC_BACKEND_RPC_URL);
  const delegateSeedPhrase = process.env.NEXT_PRIVATE_DELEGATE_SEED_PHRASE;

  if (!delegateSeedPhrase) {
    res.status(500).json('Delegate seed phrase is not set');
    return null;
  }

  const signer = Wallet.fromMnemonic(delegateSeedPhrase).connect(provider);

  return signer;
}

```

Here is the core of the delegation

* With `isPlatformAllowedToDelegate`, we check if the user has activated delegation by requesting the user graph and verifying if a delegation address has been set by the platform.
* With `getDelegationSigner`, we ensure that the platform has correctly configured all the necessary variables to instantiate the signer for delegation purposes.

## See the Full Code Implemented on Our Demo DAPP

* Service Form component: [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ServiceForm.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ServiceForm.tsx)
* Request component : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/request.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/request.ts)
* Delegate API : [https://github.com/TalentLayer-Labs/indie-frontend/tree/main/src/pages/api/delegate](https://github.com/TalentLayer-Labs/indie-frontend/tree/main/src/pages/api/delegate)
* isPlatformAllowedToDelegate and getDelegationSigner : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/api/utils/delegate.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/api/utils/delegate.ts)
