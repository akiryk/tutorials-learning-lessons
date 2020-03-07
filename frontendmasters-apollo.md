# Apollo & Graphql

## Graphql

### Operation Name

It's important to name the operation for Apollo to be able to cache.

```js
query Cat { // operationKeyWord OperationName
  cat {
    id
    name
  }
}
```

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
```

## Mutations

### Mutations in Graphql

- Mutations usually take an input, which you can find in the docs. 
- The input has a type, also in the docs
- The mutation can return data; take advantage of this. You may be able to update the app without another graphql query, so consider matching the data you get back to your queries

```js
mutation AddPet($newPet:NewPetType!) { // operationKeyWord operationName(variable: VariableType)
  addPet(input: $newPet) { // run the 'addPet' mutation; satisfy its input variable.
    id
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
  const [createPet, newPetData] = useMutation(CREATE_PET);
  
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

