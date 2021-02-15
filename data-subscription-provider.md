# DSP Notes

## dataMap
The `dataMap` is an object whose keys represent individual subscribers.
```js
const dataMap = {
    GROUP-X::item-a {
        groupName: GROUP-X,
        identifier: item-a,
        status: 'found',
        subscriptionKey: 'GROUP-X::item-a',
        dispatchSubscriptionUpdate(){}, // only added by the subscriber; a function that will be run whenever the item is updated
        data: {
            // arbitrary data returned from fetch or added by the subscriber
        }
    },
    GROUP-X::item-b {
        groupName: GROUP-X,
        identifier: item-b,
        status: 'not-found',
        subscriptionKey: 'GROUP-X::item-b',
        data: null, // items that aren't found will always have null for data
    },
    SOME-OTHER-GROUP::item21 {
        groupName: SOME-OTHER-GROUP,
        identifier: item21,
        status: 'registered',
        subscriptionKey: 'SOME-OTHER-GROUP::item21',
        data: null
    }
}
```
