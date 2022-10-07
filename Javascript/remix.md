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
    │   root.tsx
    │
    └───routes
        │   parent.tsx
        │
        └───parent
             │   nested.tsx
```

## html

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

## Forms

When you use a `form`, it is a basic form and behaves like one — e.g. it refreshes the page on submit. Progressively enhance by using the `<Form>` component from Remix to benefit from JS and also from smart fall-backs.

## Optimistic UI

Use `useTransition` to [display an optimistic UI](https://remix.run/docs/en/v1.5.1/guides/optimistic-ui#optimistic-ui) _before_ data is actually saved.

## Monitoring

[Metronome](https://metronome.sh/#pricing) is designed to work with Remix
