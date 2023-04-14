# Querying TalentLayer graph from an Application

## Using GraphQL client

### **AXIOS**

To make a subgraph request, we use Axios. Axios is a library that allows us to send HTTP requests from the browser or Node.js.
You can use Axios (or other libraries) to query the TalentLayer subgraph. You can find the documentation [here](https://axios-http.com/docs/intro)

> We will detail step by step how to query the TalentLayer subgraph using Axios and display the result on the front end

</br>

---

</br>

#### **1 - REQUEST THE SUBGRAPH**

</br>

First we need to set up the process Request (please check the [file](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/utils/graphql.ts) to learn more)

```typescript
/* eslint-disable no-console */
import axios from "axios";
import { config } from "../config";

export const processRequest = async (query: string): Promise<any> => {
  try {
    return await axios.post(config.subgraphUrl, { query });
  } catch (err) {
    console.error(err);
    return null;
  }
};
```

This asynchronous function takes a query string as a parameter, sends it as a POST request to a configured subgraph URL using the axios library, and returns the response data. If an error occurs during the request, the error is logged to the console, and the function returns null

</br>

---

</br>

#### **2 - BUILD THE QUERY**

</br>

Now we can use the processRequest function to query the subgraph.
Let's build a query! For example, if you want to get the user informations based on the user id, we can use the following query:

```typescript
export const getUserById = (id: string): Promise<any> => {
  const query = `
    {
      user(id: "${id}") {
        id
        address
        handle
        rating
        numReviews
        updatedAt
        createdAt
        description {
          about
          role
          name
          country
          headline
          id
          image_url
          video_url
          title
          timezone
          skills_raw
        }
      }
    }
    `;
  return processRequest(query);
};
```

You can test multiple queries on the [subgraph playground](https://thegraph.com/hosted-service/subgraph/talentlayer/talentlayer-polygon)
We will detail in the next queries documentation file how to build your own queries and what kinf of data you can get from the TalentLayer subgraph.

</br>

---

</br>

#### **3- BUILD YOU HOOK**

</br>

Now that we have our query, we can use it in a hook to get the user information.

```typescript
import { useState, useEffect } from "react";
import { getUserById } from "../queries/users";
import { IUser } from "../types";

const useUserById = (userId: string): IUser | null => {
  const [user, setUser] = useState<IUser | null>(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await getUserById(userId);
        if (response?.data?.data?.user) {
          setUser(response.data.data.user);
        }
      } catch (err: any) {
        // eslint-disable-next-line no-console
        console.error(err);
      }
    };
    fetchData();
  }, [userId]);

  return user;
};

export default useUserById;
```

This code defines a custom React hook called **useUserById** , which accepts an **id** parameter and returns a user object or null. It calls the **getUserById** function module to fetch user data by id (detailed just above). If the data is successfully fetched, the user state is updated with the retrieved user object. In case of an error, the error is logged to the console. The custom hook returns the user object, making it easy to use within other components.

Please find the code[here](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/hooks/useUserById.ts)

</br>

---

</br>

#### **3- DIPLAY DATA ON THE FRONT END**

</br>

```typescript
// we import the hook
import useUserById from "../hooks/useUserById";

.......
........
.........

// we call the hook and pass the user id as a parameter and we store the object response in a variable
const userDescription = user?.id ? useUserById(user?.id)?.description : null;

.......
........
.........

return (
// we display the data
<p className='text-gray-900 font-medium'>{userDescription?.about}</p>
<p className='text-gray-900 text-xs'>{userDescription?.title}</p>
)

```

Please find the full code [here](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/components/UserDetail.tsx)

</br>

> Let's now see how build different querie
