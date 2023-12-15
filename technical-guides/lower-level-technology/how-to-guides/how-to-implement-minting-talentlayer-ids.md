---
description: >-
  Minting a TalentLayer ID is the first step that your users will need to do
  when registering for an account on your platform.
---

# How to implement minting TalentLayer IDs?

## Good to Know

In this example, we will use reactJS, Ether.js and formik to handle the form on the frontend. You will find a full code example with all imports at the end of tutorial.&#x20;

## ① Create a Form for Choosing a TalentLayer ID Handle

_The user will create his handle._

```javascript
// Imports can be find in the full example at the end of the tutorial

interface IFormValues {
  handle: string;
}

const initialValues: IFormValues = {
  handle: '',
};

function TalentLayerIdForm() {
  const validationSchema = Yup.object().shape({
    handle: Yup.string()
      .min(2)
      .max(10)
      .when('isConnected', {
        is: account && account.isConnected,
        then: schema => schema.required('handle is required'),
      }),
  });

  
  const onSubmit = async (
    submittedValues: IFormValues,
    { setSubmitting }: { setSubmitting: (isSubmitting: boolean) => void },
  ) => {
    // We will handle submit here on the next step
  };

  return (
    <Formik initialValues={initialValues} onSubmit={onSubmit} validationSchema={validationSchema}>
      {({ isSubmitting }) => (
        <Form>
            <Field
                type='text'
                placeholder='Choose your handle'
                id='handle'
                name='handle'
                required
            />
            <button type='submit'>Submit</button>
        </Form>
      )}
    </Formik>
  );
}

export default TalentLayerIdForm;
```

**Bonus:** You can check if an handle is already taken and include it in the form validation by using a subgraph query.

```javascript
export const getUserByHandle = (handle: string): Promise<any> => {
  const query = `
  {
    users(where: {handle_contains_nocase: "${handle}"}, first: 1) {
      id
    }
  }
  `;
  return processRequest(query);
};
```

## ②  Handle Submit and Post to the Blockchain

_On submit, we create a new transaction and call the mint function of the TalentLayerId contract._

```javascript
const onSubmit = async (
    submittedValues: IFormValues,
    { setSubmitting }: { setSubmitting: (isSubmitting: boolean) => void },
  ) => {
    try {
        const contract = new ethers.Contract(
            config.contracts.talentLayerId,
            TalentLayerID.abi,
            signer,
        );

        const tx = await contract.mint('1', submittedValues.handle);
        setSubmitting(false);
    } catch (error) {
        console.error(error);
    }
  };
```

## ③  Get Your New User Information With Subgraph API

_After the transaction succeeds, the new user will be viewable via our subgraph api._

```javascript
export const getUserByAddress = (address: string): Promise<any> => {
  const query = `
    {
      users(where: {address: "${address.toLocaleLowerCase()}"}, first: 1) {
        id
        address
        handle
      }
    }
    `;
  return processRequest(query);
};
```

## See the Full Code Implemented on Our Demo DAPP

* Form and submit: [https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/TalentLayerIdForm.tsx](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/Form/TalentLayerIdForm.tsx)
* processRequest utils function: [https://github.com/TalentLayer-Labs/indie-frontend/blob/00e882431f3ad820374841070b7f7fe1a8053c44/src/utils/graphql.ts](https://github.com/TalentLayer-Labs/indie-frontend/blob/00e882431f3ad820374841070b7f7fe1a8053c44/src/utils/graphql.ts)
