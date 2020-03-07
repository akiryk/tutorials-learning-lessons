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
