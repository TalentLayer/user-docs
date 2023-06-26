---
description: >-
  In this section, we will see how the user can activate or deactivate the
  delegation feature on their dashboard.
---

# User workflow

## 1 - The component

Feel free to add the activation wherever you want. Currently, it is added in a popup modal, but it will soon be moved to a dedicated setting section in the user dashboard.

```tsx
import { Provider } from '@wagmi/core';
import { ethers } from 'ethers';
import { createMultiStepsTransactionToast, showErrorTransactionToast } from '../utils/toast';

export const toggleDelegation = async (
  user: string,
  DelegateAddress: string,
  provider: Provider,
  validateState: boolean,
  contract: ethers.Contract,
): Promise<void> => {
  try {
    let tx: ethers.providers.TransactionResponse;
    let toastMessages;
    if (validateState === true) {
      tx = await contract.addDelegate(user, DelegateAddress);
      toastMessages = {
        pending: 'Submitting the delegation...',
        success: 'Congrats! the delegation is active',
        error: 'An error occurred while delegation process',
      };
    } else {
      tx = await contract.removeDelegate(user, DelegateAddress);
      toastMessages = {
        pending: 'Canceling the delegation...',
        success: 'The delegation has been canceled',
        error: 'An error occurred while canceling the delegation',
      };
    }

    await createMultiStepsTransactionToast(toastMessages, provider, tx, 'Delegation');
  } catch (error) {
    showErrorTransactionToast(error);
  }
};

```

As you can see, we have added the `addDelegate` and `removeDelegate` functions from the TalentLayerID contract. By triggering these functions, it will call the respective function with two parameters.

* `user` : is the TalentLayer user ID
* `DelegateAddress` : is the delegate address add by the platform in the .env file

## See the Full Code Implemented on Our Demo DAPP

* Delegate Modal : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Modal/DelegateModal.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Modal/DelegateModal.tsx)
* Toggle Delegation : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/contracts/toggleDelegation.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/contracts/toggleDelegation.tsx)
