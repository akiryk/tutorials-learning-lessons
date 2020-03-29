# Firebase Firestore

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
