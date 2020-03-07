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
