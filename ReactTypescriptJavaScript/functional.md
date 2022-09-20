# Functional

## Composition
Compose with reduce

```js
function compose(...fns) {
  if (!fns.length) {
    return input => input;
  }
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
Compose with recursion
```js
function composeByRecursion(...fns) {
  if (!fns.length) {
     return input => input;
  }
  if (fns.length === 1) {
    return input => fns[0](input);
  }
  const accumluatedFns = fns[0]; // the head
  const nextFn = fns[1]; // the current function
  const uncomposedFns = fns.slice(2); // the tail

  // Put the composed functions at the front of the array
  uncomposedFns.unshift(input => accumluatedFns(nextFn(input)));

  return composeByRecursion(...tail);
}
```
