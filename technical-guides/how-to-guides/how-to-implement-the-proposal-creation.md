---
description: >-
  In the Find Job section, users can create a proposal for the job they want to
  apply for. We will use and detail the use of function createProposal or
  updateProposal
---

# How to implement the proposal creation?

## Good to Know

In this example, we will use reactJS, Ether.js and formik to handle the form on the frontend. You will find a full code example with all imports at the end of tutorial.&#x20;

## ① Create a Form for the proposal creation

_The user will create a proposal for a job_ [_(ProposalForm component)_](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ProposalForm.tsx)

```tsx
// The interface for the inupt field of your form
interface IFormValues {
  about: string;
  rateToken: string;
  rateAmount: number;
  expirationDate: number;
  videoUrl: string;
}

// As we using Formik we use the validationSchema to check all the input value.
const validationSchema = Yup.object({
  about: Yup.string().required('Please provide a description of your service'),
  rateToken: Yup.string().required('Please select a payment token'),
  rateAmount: Yup.string().required('Please provide an amount for your service'),
  expirationDate: Yup.number().integer().required('Please provide an expiration date'),
});

```

Let's create our form&#x20;

```tsx
// We set up our input field to get the data to create our IPFS CID

return (
  <Formik initialValues={initialValues} onSubmit={onSubmit} validationSchema={validationSchema}>
        {({ isSubmitting }) => (
          <Form>
            <h2 className='mb-2 text-gray-900 font-bold'>For the job:</h2>
            <ServiceItem service={service} />
  
            <h2 className=' mt-8 mb-2 text-gray-900 font-bold'>Describe your proposal in details:</h2>
            <div className='grid grid-cols-1 gap-6 border border-gray-200 rounded-md p-8'>
              <label className='block'>
                <span className='text-gray-700'>about</span>
                <Field
                  as='textarea'
                  id='about'
                  rows={8}
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

## ②  Handle Submit and Post the proposal

_On submit, we create a new transaction and call the createProposal or the updateProposal for that we will need our contract instance and all the parameter including the **CID** (data stored on IPFS)_

<pre class="language-tsx"><code class="lang-tsx"><strong>const onSubmit = async (
</strong>    values: IFormValues,
    {
      setSubmitting,
      resetForm,
    }: { setSubmitting: (isSubmitting: boolean) => void; resetForm: () => void },
  ) => {
  
  /*.............................
   we proceed to different check and date formatting 
  .............................*/
  
  /*
   as we using the defender API to manage platform signature we need to get it
   as it's a parameter of the createProposal function 
   */
  const signature = await getProposalSignature({
        profileId: Number(user.id),
        cid,
        serviceId: Number(service.id),
  });

  // We need to create the CID to post some data off-chain
   const cid = await postToIPFS(
      JSON.stringify({
        about: values.about,
        video_url: values.videoUrl,
      }),
    );
    
  // We need the contract instance to call the function
  const contract = new ethers.Contract(
    config.contracts.serviceRegistry, // contract address
    ServiceRegistry.abi, // the contract ABI
    signer, // the signer
  );
  
  /*
   If a proposal existingProposal exist we call updateProposal otherwise we call 
    createProposal
  */
<strong>  const tx = existingProposal
</strong>    ? await contract.updateProposal(
        user.id,
        service.id,
        values.rateToken,
        parsedRateAmountString,
        cid,
        convertExpirationDateString,
      )
    : await contract.createProposal(
        user.id,
        service.id,
        values.rateToken,
        parsedRateAmountString,
        process.env.NEXT_PUBLIC_PLATFORM_ID,
        cid,
        convertExpirationDateString,
        signature,
      );

  
  
</code></pre>

## ③  Get the Proposal by User  With Subgraph API

_Here is an example of a Graph Query you can use to get the proposal by user_

```graphql
export const getAllProposalsByUser = (id: string): Promise<any> => {
  const query = `
      {
        proposals(where: {seller: "${id}", status: "Pending"}) {
          id
          rateAmount
          rateToken {
            address
            decimals
            name
            symbol
          }
          status
          cid
          createdAt
          seller {
            id
            handle
          }
          service {
            id
            cid
            createdAt
            buyer {
              id
              handle
            }
          }
          description {
            id
            about
            expectedHours
            startDate
            video_url
          }
          expirationDate
        }
      }
    `;
  return processRequest(query);
};gra
```

More proposal query [**here**](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/queries/proposals.ts)&#x20;

## See the Full Code Implemented on Our Demo DAPP

* Form and submit: [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ProposalForm.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/ProposalForm.tsx)
* Proposal queries : [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/queries/proposals.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/queries/proposals.ts)
* Contract: [https://github.com/TalentLayer/talentlayer-contracts/blob/main/contracts/TalentLayerService.sol](https://github.com/TalentLayer/talentlayer-contracts/blob/main/contracts/TalentLayerService.sol)
* processRequest utils function:

**GraphQL** :  [https://github.com/TalentLayer-Labs/indie-frontend/blob/00e882431f3ad820374841070b7f7fe1a8053c44/src/utils/graphql.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/00e882431f3ad820374841070b7f7fe1a8053c44/src/utils/graphql.ts)

**IPFS :** [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/utils/ipfs.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/utils/ipfs.ts)
