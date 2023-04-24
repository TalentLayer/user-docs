# Queries examples

Here, we will explore the various queries that you can create.

## Get user information by Talent Layer Id

{% tabs %}
{% tab title="Example query" %}
```graphql
{
  user(id: "59") {
    cid
    handle
    id
    numReviews
    description {
      about
      id
    }
    address
    updatedAt
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```json
{
  "data": {
    "user": {
      "cid": "QmawFHVwFggkFC5FgY2i2dDPfqDiVGvzJJAM7NyxvCAU6W",
      "handle": "martin",
      "id": "59",
      "numReviews": "1",
      "description": {
        "about": "I'm a fan of robots, time rifts and giant bionic shark movies. And all things about #Web3, #Blockchain, #NFT, #Metaverse, #DEFI etc...",
        "id": "QmawFHVwFggkFC5FgY2i2dDPfqDiVGvzJJAM7NyxvCAU6W-1681747217",
      },
      "address": "0x1caab8ded4535bf42728fea90afa7da1ac637e1e",
      "updatedAt": "1681747217"
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get the service reviews by service id

{% tabs %}
{% tab title="Example query" %}
```graphql
{
  reviews {
    description {
      content
      id
    }
    rating
    to {
      id
      handle
    }
    service {
      id
      status
    }
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```json
{
  "data": {
    "review": {
      "description": {
        "content": "Perfect!",
        "id": "QmW612hUxvg1SigPA5Y3msuBEuXfLaH3axp22dr1kwCXp8-1680027235"
      },
      "rating": "5",
      "to": {
        "id": "2",
        "handle": "migmig"
      },
      "service": {
        "id": "1",
        "status": "Finished"
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get the first 5 services informations after the 18 March with the open status

{% tabs %}
{% tab title="Example query" %}
```graphql
{
  services(first: 3, where: {createdAt_gt: "1679149214", status: Opened}) {
    id
    createdAt
    updatedAt
    status
    description {
      about
      rateAmount
      rateToken
      startDate
      title
    }
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```json
{
  "data": {
    "services": [
      {
        "id": "100",
        "createdAt": "1681996135",
        "updatedAt": "1681996135",
        "status": "Opened",
        "description": {
          "about": "We looking for a Solidity developer",
          "rateAmount": "1000000000000000000",
          "rateToken": "0x0000000000000000000000000000000000000000",
          "startDate": null,
          "title": "Solidity developer"
        }
      },
      {
        "id": "101",
        "createdAt": "1681997279",
        "updatedAt": "1681997279",
        "status": "Opened",
        "description": {
          "about": "We looking for a Rust developer",
          "rateAmount": "1000000000000000000",
          "rateToken": "0x0000000000000000000000000000000000000000",
          "startDate": null,
          "title": "Rust developer"
        }
      },
      {
        "id": "102",
        "createdAt": "1682017181",
        "updatedAt": "1682017181",
        "status": "Opened",
        "description": {
          "about": "We looking for a C++ developer",
          "rateAmount": "1000000000000000000",
          "rateToken": "0x0000000000000000000000000000000000000000",
          "startDate": null,
          "title": "C++ developer"
        }
      }
    ]
  }
```
{% endtab %}
{% endtabs %}

## Get the total gain and the platform name of the first 3 users with a rating greater than 4

{% tabs %}
{% tab title="Example query" %}
```graphql
{
  users(first: 3,where: {rating_gt: "4"}) {
    handle
    id
    numReviews
    platform {
      id
      name
    }
    totalGains {
      totalGain
    }
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```json
{
  "data": {
    "users": [
      {
        "handle": "thomas",
        "id": "1",
        "numReviews": "1",
        "platform": {
          "id": "4",
          "name": "WorkX"
        },
        "totalGains": [
        {
            "totalGain": "14000000000"
          }
        ]
      },
      {
        "handle": "mattia",
        "id": "11",
        "numReviews": "1",
        "platform": "6clover",
        "totalGains": [
          {
            "totalGain": "100000000"
          }
        ]
      },
      {
        "handle": "migmig",
        "id": "2",
        "numReviews": "1",
        "platform": {
          "id": "4",
          "name": "indie"
        },
        "totalGains": [
          {
            "totalGain": "1000000000000000000"
          }
        ]
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
As you can see, you are not limited in your query building. Please feel free to contact us if you cannot find or build exactly what you need.
{% endhint %}
