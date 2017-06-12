# Relationships in a No-SQL (MongoDB) Database

**There is no rule when embedding data in MongoDB, but overall, we should observe:**  

  •	 Whether we have a one-to-one relationship between documents.  
  •	 Whether we have a one-to-many relationship between documents, and
whether the "many" part of the relationship is very dependent of the "one" part. This means, for instance, that every time we present the "one" part, we will also present the "many" part of the relationship.  

**There is no rule for references using MongoDB, but overall, we should observe:**  

  •	 Whether we are duplicating the same information many times while embedding data (this shows poor reading performance)  
  •	 Whether we need to represent many-to-many relationships  
  •	 Whether our model is a hierarchy  

**To Embed or to Reference**  

This section will present you with patterns that illustrate when to embed or when to reference documents. Until now, we have considered as a deciding factor:  
  •	 Whether consistency is the priority  
  •	 Whether read is the priority  
  •	 Whether write is the priority  
  •	 What update queries we will make  
  •	 Document growth  
  
#### One to One Relationships

Most of the time one-to-one relationships are modeled using an embedded document, especially if that one document is contained by the other.

For example, take the following data:
```
user
{
  "_id": 5478329cb9617c750245893b,
  "username": "thinkfuluser",
  "password": "userpassword",
}
user_profile
{
  "email": "thinkful@example.com",
  "first_name": "Joe",
  "last_name": "Blow",
  "address": "56 hidden valley ln"
}
```

This would be best modeled by embedded documents:  

```
user
{
  "_id": 5478329cb9617c750245893b,
  "username": "thinkfuluser",
  "password": "userpassword",
  "profile": {
    "email": "thinkful@example.com",
    "first_name": "Joe",
    "last_name": "Blow",
    "address": "56 hidden valley ln"
  }
}
```

Advantages of using embedded documents is that all queries to the parent `user` will return the embedded `profile` data as well, much the same as a join would in a SQL database.  

#### One-to-Many

In a **One-to-Many** relationship we have to consider the *"many"* side of the relationship.  If the *many* side should be displayed with its parents, then embedding is the way to go, otherwise, referencing.  

Take the following data for an example:  
```
user
{
  "_id": 1,
  ...
  ...
  ...
}
address
{
  "_id": 1736354784,
  "customer_id": 1,
  "type": "billing"
  ...
  ...
  ...
}
{
  "_id": 1537484934,
  "customer_id": 1,
  "type": "shipping",
  ...
  ...
  ...
}
{
  "_id": 544749474,
  "customer_id": 1
  "type": "shipping",
  ...
  ...
  ...
}
```

This data would be better off being modeled as embedded documents:  
```
user
{
  "_id": 1,
  ...
  ...
  ...
  "billingAddress": [
  {
    ...
    ...
    ...
  }
  ],
  "shippingAddress": [
  {
    ...
    ...
    ...
  },
  {
    ...
    ...
    ...
  }
  ]
}
```  

#### Many-to-Many

The best way to outline the options for **Many-to-Many** relationships is to use an example of `users` and `groups`.  

```
user
{
  "_id": 1,
  "username": "user1",
  ...
  ...
},
{
  "_id": 2,
  "username": "user2",
  ...
  ...
},
{
  "_id": 3,
  "username": "user3",
  ...
  ...
}

groups
{
  "_id": 1,
  "name": "group1",
  ...
},
{
  "_id": 2,
  "name": "group2"
  ...
}
```

We can store the **relationship** in the `user` document, as follows:  
```
user
{
  "_id": 1,
  "username": "user1",
  "groups": [
    {
      "_id": 1,
      "name": "group1"
    },
    {
      "_id": 2,
      "name": "group2"
    }
  ]
},
{
  "_id": 2,
  "username": "user2",
  "groups": [
    {
      "_id": 1,
      "name": "group1"
    }
  ]
}

group
{
  "_id": 2,
  "name": "group1",
  ...
}
{
  "_id": 2,
  "name": "group2",
  ...
}
```  

Or we can store it in the `group` document, as follows:

```
user
{
  "_id": 1,
  "username": "user1"
}
{
  "_id": 2,
  "username": "user2"
}

group
{
  "_id": 1,
  "name": "group1",
  "users": [
    {
      "_id": 1,
      "username": "user1"
    }
    {
      "_id": 2,
      "username": "user2"
    }
  ]
}
{
  "_id": 2,
  "name": "group2",
  "users": [
    {
      "_id": 1,
      "username": "user1"
    }
  ]
}
```

Or we can store the relationship in both documents, as follows:
```
user
{
  "_id": 1,
  "username": "user1",
  "groups": [1, 2]
}
{
  "_id": 2,
  "username": "user2",
  "groups": [1]
}

group
{
  "_id": 2,
  "name": "group1",
  "users": [1,2]
}
{
  "_id": 2,
  "name": "group2",
  "users": [1]
}
```
