# Apollo & Graphql

## Start a client side apollo project:

### HttpLink

```js
import { HttpLink } from 'apollo-link-http'

// use HttpLink to create a link to a graphql server endpoint
const link = new HttpLink({
  uri: "http://localhost:4000",
})
```

### Cache

```js
import { inMemoryCache } from 'apollo-cache-inmemory'

const cache = new inMemoryCache()
```

### Client

```
import { ApolloClient } from 'apollo-client'

const client = new ApolloClient({
  cache,
  link
});

// Instead of using the Apollo hook (below), it's possible call a query or mutation and wait by using client directly:
client.query(SOME_QUERY)
  .then(data => {
    // etc
```

## Graphql Review

### Queries

- Queries take the `query` operation keyword followed by an operation name
- While not required, it's important to use the operation name for Apollo to cache.

```js
query Cat { // operationKeyWord OperationName
  cat {
    id
    name
  }
}
```

### Mutations in Graphql

- Mutations usually take an input, which you can find in the docs. 
- The input has a type, also in the docs
- The mutation can return data; take advantage of this. You may be able to update the app without another graphql query, so consider matching the data you get back to your queries

```js
mutation AddPet($newPet:NewPetType!) { // operationKeyWord operationName(variable: VariableType)
  addPet(input: $newPet) { // run the 'addPet' mutation; satisfy its input variable.
    id // get back id and name since that's what we're querying for in the above query
    name
  }
}
```

### Using Mutations in React with Apollo

- Use the `useMutation` hook to get a function and an object with loading, error, data.
- Call the useMutation function and pass it a gql mutation.
- 

```js
const {useMutation} from '@apollo/react-hooks';

const CREATE_PET = (the addPet mutation above...)

const MyComponent = () => {
  // createPet is the mutation function
  // newPetData is an object with data, error, and loading.
  const [createPet, newPet] = useMutation(CREATE_PET);
  
  const handleSubmit = input => {
    createPet({
      variables: { // the variables option contains any required inputs for the mutation
        newPet: {  // we call the variable 'newPet' (without $) because that's what the mutation calls this input
          name: input.name, // The newPet input requires a NewPetType, which requires a name and a type. 
          type: input.type
        }
      });
  }
  
  if (newPet.loading) {
     return <Loader />
  }
  
  if (newPet.error) {
    return <ErrorMessage error={error} />
  }
  
  return ( 
    // etc.
}
 ```

### Update Local Cache after a mutation

When you make a mutation to a single item, it will automatically update the cache. For example, if you have a `pet` query that gets a single pet and a `updatePet` mutation that updates a single pet by ID, the cache will update as soon as mutation returns. 

However, if you are mutating a list — e.g. a an array of pets or any collection at all — you need to take charge of updating the cache yourself. There a several ways to do that described in [Apollo docs](https://www.apollographql.com/docs/react/data/mutations/). However, the best way for many cases is to use the update option on the `useMutation` hook.

```js
const [createPet, newPet] = useMutation(CREATE_PET, {
  // update takes cache from the client and a data object.
  // The data object takes the mutation's returned data. The name (addPet) must match the name of your mutation.
  update(cache, {data: { addPet }}) {
    // get the current data in the cache
    const data = cache.readQuery({ query: ALL_PETS }); 
    // update the cache
    cache.writeQuery({ 
      query: ALL_PETS,
      data: { pets: [addPet, ...data.pets] } // e.g. prepend addPet (the name of your mutation) to data
    })
  }
});
```

### Optimistic Update

Rather than waiting for a server response when making a mutation, Apollo will optimistically update the UI if you give it the right data.

- Use the `optimisticResponse` property ([see docs](https://www.apollographql.com/docs/react/performance/optimistic-ui/)
- Add it to either your submit handler or to the mutation hook
    - if you add it to the mutation hook, it will be used every single time that mutation is called
    - if you add it to your submit handler, you can use data from the inputs to more accurately reflect the data returned from server
- Either way, you need to accurately reflect the way data will be returned from the server. Not only must you give it fields such as `id` and `name`, you must give it values for otherwise hidden fields, such as `__typename`.
- If you use fragment in the query, you'll need to tell optimisticResponse that there is a fragment.

```js
// Attach to the submit handler, specifically where we call the mutation.
const handleSubmit = input => {
  createPet({
    variables: {
      newPet: {
        name: input.name,
        type: input.type
      }
    },
    optimisticResponse: {
      __typename: 'Mutation', 
      addPet: { // the mutation's name
        __typename: 'Pet',
        id: Date.now().toString(), // we don't know what this will be, but we know it will be a string (ID type is a string)
        name: input.name,
        type: input.type, 
        img: 'some-placeholder.jpg'
      }
    }
  })
}
```

### Client Side Schemas

Apollo enables us to manage local state much like Redux. We do this by extending query types to add whatever data we want, locally, to the types that are stored on the server. 

1. Create a local schema (see below)
2. Add schema as additional arguments when making the client
3. Use properties of the local schema by adding a directive, `@client`

For example, we have a `User` type like so:
```
User
  id: ID!
  username: String!
  pets: [Pet]!
```

We define the local state with a schema, made of two parts:

- type definitions
- resolvers

```js
// client.js

// type definitions that extend the types from the server
const typeDefs = gql`
    extend type User {
        age: Int
    }
`

// Resolvers
const resolvers = {
  // resolver maps directly to the user type and to the fields we want to get data for.
  User: {
    age() {
        return 35;
    }
  }
}

// add to client, e.g.
const client = new ApolloClient({ 
  link,
  cache,
  resolvers,
  typeDefs
})

// when you want to access the age property,
const ALL_PETS = gql`
    query AllPets {
      pets {
        id
        name
        type
        user {
          id
          age @client
        }
      }
    }
`
```

### Fragments

```
const PETS_FIELDS = {
  fragment PetsFields on Pet {
       id
        name
        type
        user {
          id
          age @client
        }
    }
 }
 
 // use the fragment
 const All_Pets = gql`
     query allPets {
         pets {
            ...PetsFields
         }
      }
      ${PETS_FIELDS}
`
```
