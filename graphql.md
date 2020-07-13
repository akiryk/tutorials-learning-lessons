# GraphQL tips and tricks and shortcuts

## Queries

```
export const getSomething = gql`
  query getSomething($someId: Int64) {
    theThing(input: {id: $someId}) {
      id
      name
    }
  }
}`;
```

You can now use fetchQuery with this query as in:
```
fetchQuery({
  query: registryItemsQuery,
  variables: {
    someId: 121312,
  })
  .then(() => {
    // etc
  });
```
