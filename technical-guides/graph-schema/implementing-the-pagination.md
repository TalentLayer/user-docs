# Implementing the pagination

In this guide, we'll explore how to implement pagination in your application using GraphQL queries. Pagination is essential for handling large data sets, providing a user-friendly way to navigate and interact with the information. We'll cover key concepts and techniques, enabling you to create efficient, scalable, and seamless user experiences with TalentLayer Graph



## 1-Set and adapt your query

```tsx
export const getUsers = (
  numberPerPage?: number,
  offset?: number,
  searchQuery?: string,
): Promise<any> => {
  const pagination = numberPerPage ? 'first: ' + numberPerPage + ', skip: ' + offset : '';
  let condition = ', where: {';
  condition += searchQuery ? `, handle_contains_nocase: "${searchQuery}"` : '';
  condition += '}';

  const query = `
    {
      users(orderBy: rating, orderDirection: desc ${pagination} ${condition}) {
        id
        address
        handle
        userStats {
          numReceivedReviews
        }
        rating
      }
    }
    `;
  return processRequest(query);
};
```

The function first construct a pagination string based on the provided `numberPerPage` and `offset` parameters. If `numberPerPage` is not provided, the pagination string will be empty, which means that the query will fetch all users without pagination.

Next, the function constructs a conditional string that will be used in the GraphQL query to filter the users based on the provided `searchQuery`. If no `searchQuery` is provided, the conditional string will only contain an empty object.

Then we build the query with our two parameters =>  **pagination** and **condition**

Please find the code [here](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/queries/users.ts)

### Other type of query for pagination

As you can see in the query just below is that we add to parameter **StartDate** and **EndDate** that will allow us to set up a filter by date on our front end

```tsx
export const getPaymentsForUser = (
  userId: string,
  numberPerPage?: number,
  offset?: number,
  startDate?: string,
  endDate?: string,
): Promise<any> => {
  const pagination = numberPerPage ? 'first: ' + numberPerPage + ', skip: ' + offset : '';

  const startDataCondition = startDate ? `, createdAt_gte: "${startDate}"` : '';
  const endDateCondition = endDate ? `, createdAt_lte: "${endDate}"` : '';

  const query = `
    {
      payments(where: {
        service_: {seller: "${userId}"}
        ${startDataCondition}
        ${endDateCondition}
      }, 
      orderBy: createdAt orderDirection: desc ${pagination} ) {
        id, 
        rateToken {
          address
          decimals
          name
          symbol
        }
        amount
        transactionHash
        paymentType
        createdAt
        service {
          id, 
          cid
        }
      }
    }
    `;
  return processRequest(query);
};
```

## 2-Adapt your hook

We add a few state variable and parameter in the **useUsers** hook

```tsx
import { useEffect, useState } from 'react';
import { getUsers } from '../queries/users';
import { IUser } from '../types';

const useUsers = (
  searchQuery?: string,
  numberPerPage?: number,
): { hasMoreData: boolean; loading: boolean; users: IUser[]; loadMore: () => void } => {
  const [users, setUsers] = useState<IUser[]>([]);
  const [hasMoreData, setHasMoreData] = useState(true);
  const [loading, setLoading] = useState(false);
  const [offset, setOffset] = useState(0);

  useEffect(() => {
    setUsers([]);
    setOffset(0);
  }, [searchQuery]);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const response = await getUsers(numberPerPage, offset, searchQuery);

        if (offset === 0) {
          setUsers(response.data.data.users || []);
        } else {
          setUsers([...users, ...response.data.data.users]);
        }

        if (numberPerPage && response?.data?.data?.users.length < numberPerPage) {
          setHasMoreData(false);
        } else {
          setHasMoreData(true);
        }
      } catch (err: any) {
        // eslint-disable-next-line no-console
        console.error(err);
      } finally {
        setLoading(false);
      }
    };
    fetchData();
  }, [numberPerPage, offset, searchQuery]);

  const loadMore = () => {
    numberPerPage ? setOffset(offset + numberPerPage) : '';
  };

  return { users, hasMoreData: hasMoreData, loading, loadMore };
};

export default useUsers;

```

1. `hasMoreData`: This state variable is a boolean that indicates whether there are more users to fetch. It is initially set to `true`, which means that when the component is first rendered, it assumes there is more data to load. As data is fetched, this state variable will be updated based on the length of the fetched data. If the length of the fetched data is less than the specified `numberPerPage`, it sets `hasMoreData` to `false`, indicating that there are no more users to fetch. it allow you to display a button or a message.
2. `loading`: This state variable is a boolean that indicates whether data is being fetched. It is initially set to `false`. it allow you to display a loader during the fetch process.
3. `offset`: This state variable is a number that represents the pagination offset for the users list. It is initially set to `0`. When the `loadMore` function is called, the `offset` is updated by adding the value of `numberPerPage` to the current offset. The updated offset is then used in the `getUsers` function to fetch the next set of users.
4. `numberPerPage` is the element number you want to display per page, this parameter will be set in the component

Please find the code [here](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/hooks/useUsers.ts)

## 3-Set up the pagination in your component

First we need to set up the parameter needed for **useUsers** call

```tsx
const PAGE_SIZE = 36;
```

will the element number display per page

Then we call the hook **useUsers** and destructure the return object to get users, hasMoreData, loading and loadMore

```tsx
const { users, hasMoreData, loading, loadMore } = useUsers(
    searchQuery?.toLocaleLowerCase(),
    PAGE_SIZE,
 );
```

You map your users oject and display all the data you want in a dedicated component.

```tsx
 <div className='grid grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-4'>
  {users.map((user, i) => {
    return <UserItem user={user} key={i} />;
   })}
 </div>
```

Then  we add a button who call **loadMore**, you can check the hook **useUsers** with the loadMore function that will trigger setOffset.

```tsx
<button
  type='submit'
  className={`......`}
  disabled={!hasMoreData}
  onClick={() => loadMore()}>
  Load More
</button>
```

Please find the code [here ](https://github.com/TalentLayer-Labs/indie-frontend/blob/main/src/pages/Talents.tsx)
