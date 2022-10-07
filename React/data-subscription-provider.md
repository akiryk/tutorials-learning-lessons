# DSP Notes

## dataMap
The `dataMap` is an object whose keys point to objects representing individual subscribers. Each individual subscriber object has a shape like the following:
```js
[SUBSCRIPTION_KEY]: {
  groupName: string, 
  identifier: string,
  status: string // (found, not-found, error, or registered)
  subscriptionKey: string,
  data: {
      // arbitrary data returned from fetch or added by the subscriber
  }
}
```

The dataMap object itself looks like this:
```js
const dataMap = {
    [SUBCRIPTION_KEY_1]: {},
    [SUBCRIPTION_KEY_2]: {},
    [SUBCRIPTION_KEY_3]: {},
}
```
