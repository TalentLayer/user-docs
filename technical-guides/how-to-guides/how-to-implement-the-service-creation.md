---
description: >-
  In the Post Job section, users can create a service. We will use and detail
  the function createService
---

# How to implement the service creation?

## Good to Know

In this example, we will use reactJS, Ether.js and formik to handle the form on the frontend. You will find a full code example with all imports at the end of tutorial.&#x20;

## ① Create a Form for the service creation

_The user will create a service (_[_ServiceForm component_](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ServiceForm.tsx)_)_

```tsx
// The interface for the inupt field of your form
interface IFormValues {
  title: string;
  about: string;
  keywords: string;
  rateToken: string;
  rateAmount: number;
}

// As we using Formik we use the validationSchema to check all the input value
const validationSchema = Yup.object({
    title: Yup.string().required('Please provide a title for your service'),
    about: Yup.string().required('Please provide a description of your service'),
    keywords: Yup.string().required('Please provide keywords for your service'),
    rateToken: Yup.string().required('Please select a payment token'),
    rateAmount: Yup.number()
      .required('Please provide an amount for your service')
      .when('rateToken', {
        is: (rateToken: string) => rateToken !== '',
        then: schema =>
          schema.moreThan(
            selectedToken
              ? FixedNumber.from(
                  ethers.utils.formatUnits(
                    selectedToken?.minimumTransactionAmount as BigNumberish,
                    selectedToken?.decimals,
                  ),
                ).toUnsafeFloat()
              : 0,
            `Amount must be greater than ${
              selectedToken
                ? FixedNumber.from(
                    ethers.utils.formatUnits(
                      selectedToken?.minimumTransactionAmount as BigNumberish,
                      selectedToken?.decimals,
                    ),
                  ).toUnsafeFloat()
                : 0
            }`,
          ),
      }),
  });

```

Let's create our form&#x20;

```tsx
return (
  <Formik initialValues={initialValues} onSubmit={onSubmit} validationSchema={validationSchema}>
    {({ isSubmitting, setFieldValue }) => (
      <Form>
        <div className='grid grid-cols-1 gap-6 border border-gray-200 rounded-md p-8'>
          <label className='block'>
            <span className='text-gray-700'>Title</span>
            <Field
              type='text'
              id='title'
              name='title'
              className='mt-1 mb-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50'
              placeholder=''
            />
            <span className='text-red-500'>
              <ErrorMessage name='title' />
            </span>
          </label>

          <label className='block'>
            <span className='text-gray-700'>About</span>
            <Field
              as='textarea'
              id='about'
              name='about'
              className='mt-1 mb-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50'
              placeholder=''
            />
            <span className='text-red-500'>
              <ErrorMessage name='about' />
            </span>
          </label>
          ....................
          ....................
          
        /*
         Formik will catch the submit button and trigger the onSubmit function
        in the next section
        */ 
        <SubmitButton isSubmitting={isSubmitting} label='Post' />
  );

```

## ②  Handle Submit and Post the service

_On submit, we create a new transaction and call the createService for that we will need our contract instance and all the parameter including the **CID** (offchain data stored on IPFS)_

```tsx
const onSubmit = async (
    values: IFormValues,
    {
      setSubmitting,
      resetForm,
    }: { setSubmitting: (isSubmitting: boolean) => void; resetForm: () => void },
  ) => {
  
  /*.............................
   we proceed to different check and date formatting 
  .............................*/
  
  /*
   as we using the defender API to manage signature we need to get it
   as it's a parameter of the service creation function 
   */

  // Get platform signature
  const signature = await getServiceSignature({ profileId: Number(user?.id), cid });

  
  // We need to create the CID to post some data off-chain
   const cid = await postToIPFS(
        JSON.stringify({
          title: values.title,
          about: values.about,
          keywords: values.keywords,
          role: 'buyer',
          rateToken: values.rateToken,
          rateAmount: parsedRateAmountString,
      }),
    );
    
  // We need the contract instance to call the function
  const contract = new ethers.Contract(
    config.contracts.serviceRegistry,
    ServiceRegistry.abi,
    signer,
  );
  
  
  // we call the createService function
  const tx = await contract.createService(
      user?.id,
      process.env.NEXT_PUBLIC_PLATFORM_ID,
      cid,
      signature,
    );

/*............................. */
    
```

## ③  Get the Proposal by User  With Subgraph API

_Here is an example of a Graph Query you can use to get the service by id_

```graphql
export const getServiceById = (id: string): Promise<any> => {
  const query = `
    {
      service(id: "${id}") {
        ${serviceQueryFields}
        description {
          ${serviceDescriptionQueryFields}
        }
      }
    }
    `;
  return processRequest(query);
};
```

## See the Full Code Implemented on Our Demo DAPP

* Form and submit: [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ProposalForm.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ProposalForm.tsx)
* Services query: [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/queries/services.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/queries/services.ts)
* Contract: [https://github.com/TalentLayer/talentlayer-contracts/blob/main/contracts/TalentLayerService.sol](https://github.com/TalentLayer/talentlayer-contracts/blob/main/contracts/TalentLayerService.sol)
* processRequest utils function:

**GraphQL** :  [https://github.com/TalentLayer-Labs/indie-frontend/blob/00e882431f3ad820374841070b7f7fe1a8053c44/src/utils/graphql.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/00e882431f3ad820374841070b7f7fe1a8053c44/src/utils/graphql.ts)

**IPFS :** [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/utils/ipfs.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/utils/ipfs.ts)
