# Firebase Firestore

## Security Rules

**The only applies when not using server libraries**

If using REST endpoints or server client libraries for Firestore, none of these rules apply. Instead use [Identify and Access Management tools](https://cloud.google.com/firestore/docs/security/iam)

**Matching** 

The basic structure of a rule begins with a path, e.g.
```
match /databases/{database}/document`
```
This says to match any document found anywhere that is
- in the databases path
- in a database of any name — curly braces are just a wildcard, so this would match "funfunretro" or anything else

The matches can nest but they do not cascade:
```
match /databases/{database}/document {`
  allow read
  match /restaurants/{restaurantId} {
    match /reviews/{reviewId} {
```
The `allow read` rule will not cascade and apply to reviews just because they are nested; the reviewId rules will be default unless we specify otherwise. Why nest then? 
- Helps organize our rules for easier dev experience
- It allows us access outer variables down the nest

```
match /databases/{database}/document {`
  allow read
  match /restaurants/{restaurantId} {
    match /reviews/{reviewId} {
      // we can access the restaurantId here, eg.
      allow write: if restaurantId == "1234"
```

**The Path Wildcard** 

```
match /databases/{database}/document {`
  match /users/{restOfPath=**} {
    // any rule here will match any document in users collection
    // and also any document in any sub collection e.g.
    // users/userId_123/history/history_123 will match
```

**Rule Precedence** 
```
match /databases/{database}/document {`
  match /users/{restOfPath=**} {
    allow read;
    match /users/{userId}/privateData/{privateDoc} {
    // this won't apply because the path is already set to read above
      allow read: if false; 
```

**Actions**

- Get
- List
    - `allow read;` can handle `get` and `list`
- Create
- Delete
- Update
  - `allow write;` can handle the three above

Get and List can be handled together

Make something completely public
`allow read;` or `allow read: if true;` These rules are identical

**Applying Logic**

Sometimes, you'll just allow or prohibit for everyone no matter what, e.g .`allow read;`. More often, you'll apply logic based on these three conditions

- Request data (the request object)
- Target documents
- Some other document 

The Request object is made of
- auth: contains info about the signed in user, e.g.
  - `request.auth != null` checks if they are a signed in user
  - `request.auth.uid` the user id
  - `request.auth.token.email` data from the token
  - `request.auth.token.email_verified` is the email address verified
- resource: info about the document that the user is trying to write to
  - It's a map to any field in the data
  - Access fields via `data`, as in: `request.resource.data`
  - access individual fields like `request.resource.data.score` (or `data["score"]`)



## Functions

- Create a function in the functions directory

## Graphql

### Setup The App

Assuming you are set up already with Firebase:
- `npm install apollo-server-express express graphql`
- Initialize your app:

```js
// index.js
const functions = require('firebase-functions');
const admin = require('firebase-admin');

var serviceAccount = require('../serviceAccountKey.json');

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount),
  databaseURL: 'https://funfunretro.firebaseio.com',
});

const { ApolloServer } = require('apollo-server-express');
const express = require('express');
const app = express();
```

### Create TypeDefs

In this example, we can query for a single board or for a list of boards. 

```js
// schema.js

const { gql } = require('apollo-server-express');

const typeDefs = gql`
  type Board {
    name: String
    desc: String
  }
  type Query {
    boards: [Board]
    board(id: ID!): Board
  }
`;

module.exports = { typeDefs };
```

### Create Resolvers

The list of boards requires an array, so we create and return an array with the boards we get from our async request.

- The `collection` method returns a `QuerySnapshot`
- In order to get the data we want, we need to either use the snapshot's `forEach` method or its `docs` property
- `forEach` iterates over the docs
- `docs` gives us a direct refrence to the list of documents in the collection

```js
// resolvers.js

const admin = require('firebase-admin');

module.exports = {
  Query: {
    boards: async () => {
      try {
        const boards = await admin
          .firestore()
          .collection('boards')
          .get();
        const arrayOfBoards = boards.docs.map(board => {
          return {
            name: board.data().name,
            desc: board.data().desc,
          };
        });
        console.log(arrayOfBoards);
        return arrayOfBoards;
      } catch (err) {
        console.log(err);
      }
  ```
  
  Note that we don't need to be so explicit, we could more succinctly say:

```js
// since board.data() gives us an object with name and desc, we don't need to be explicit
return boards.docs.map(board => board.data()
```

If you'd rather not use async/await, just make sure you return the result, as in:

```js
 Query: {
    boards: () => {
        return admin.firestore().collection('boards').get().then( // etc etc
```
