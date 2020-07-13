# GraphQL tips and tricks and shortcuts

## Queries

```
export const getSomething = gql`
  query getSomething($someId: Int64) {
      whatever(input: {id: $someId}) {
          id
          name
        }
      }
    }
  }
`;
```
