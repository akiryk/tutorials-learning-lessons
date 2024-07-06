# Solutions

1
```js
function initialize2DArray(options, fn) {
  return Array.from( 
    { length: options.lengthOfFirstDimension },
    () => Array.from( 
      {length: options.lengthOfSecondDimension}, fn))
}

```
