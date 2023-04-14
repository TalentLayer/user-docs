# Queries and response examples

## **Querying Services**

#### Querying Services with their related description

Any of the attributes associated with the entities can be queried.&#x20;

```graphql
{
  services {
    id
    createdAt
    updatedAt
    description {
      id
      title
      about
    }
  }
}
```

#### Filtering Services Based On Different Attributes

Queries can also be ordered by and limited in number based on the values of different attributes.

```graphql
# Get last 5 opened services with their offchain data for the platform 1
{
  services(
    orderBy: createdAt
    orderDirection: desc
    first: 5
    where: { status: Opened, platform: "1" }
  ) {
    id
    createdAt
    updatedAt
    status
    platform {
      id
    }
    buyer {
      id
      handle
      numReviews
    }
    description {
      id
      title
      about
      startDate
      expectedEndDate
      keywords_raw
      rateToken
      rateAmount
    }
  }
}
```

{% hint style="info" %}
For more information about sorting, pagination, and filtering please check out [The Graph GraphQL API documentation](https://thegraph.com/docs/en/querying/graphql-api/).
{% endhint %}

#### Fulltext Search for ServiceDescription

The TalentLayer Subgraph further offers a fulltext search feature that can be used to make more advanced text searches.&#x20;

The fulltext search allows using operators to query service descriptions based on text. For example, all the services that has a description that contains either the word `hadhat` or the word `development` in the field `title` or in the field `keywords_raw` can be found using the followng query:

```graphql
{
  serviceDescriptionSearchRank(text: "hardhat | development") {
    title
    about
    keywords_raw
    service {
      id
    }
  }
}
```

{% hint style="info" %}
For more information on which operators are allowed and how to use them, please check out the Graph's [documentations on fulltext search queries](https://thegraph.com/docs/en/querying/graphql-api/#fulltext-search-queries).
{% endhint %}
