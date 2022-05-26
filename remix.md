# Remix

## Jokes Tutorial
https://remix.run/docs/en/v1/tutorials/jokes#expected-errors

## Quick Bites!
[Nested routes description](https://blog.logrocket.com/understanding-routes-route-nesting-remix/) 

```sh
# this enables going to /parent/nested
remix-project
│   README.md
│
└───app
│   │   root.tsx
│   │
│   └───routes
│   │   │   parent.tsx
│   │   │
│   │   └───parent
│   │   │   │   nested.tsx
```

## `HTML`
You are responsible for your markup. In `root.tsx`, you'll see the `<html>` tags. This is on you. Do you want JS? Then you need to add it!
```js
import {Scripts} from '@remix-run/react';

return (
  <html>
    // etc
    <body>
      {children}
      <Scripts />
    </body
  </html>
)
```
