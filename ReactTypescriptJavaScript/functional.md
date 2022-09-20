# Functional

## Composition
Example compose function 

```js
function compose(...fns) {
  const _compose = fns.reduce((accumulator, currentValue) => {
    /*
     * On first iteration:
     * accumulator will be the first item in array of fns
     * currentValue will be the second item in array of fns
     *
     * After n iterations:
     * accumulator will be the current set of nested arrays
     * currentValue will be the nth function
     */
    return input => accumulator(currentValue(input))
  });
  return input => _compose(input);
}
```
