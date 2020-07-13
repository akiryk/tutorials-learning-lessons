# GraphQL tips and tricks and shortcuts

## Queries

```json
export const registryItemsQuery = gql`
  query getRegistryItems($registryId: Int64) {
      registry(input: {id: $registryId}) {
        registries {
          id
          name
          urlSlug
          items {
            listId
            itemConnection {
              totalCount
              ...pageInfo
              edges {
                ...node
                cursor
              }
            }
          }
        }
      }
    }
  }
`;
```
