# Functional

## Composition
Example compose function 

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
Example compose useing recursion
```js
function composeByRecursion(...fns) {
  if (!fns.length) {
     return input => input;
  }
  if (fns.length === 1) {
    return input => fns[0](input);
  }
  const head = fns[0];
  const next = fns[1];
  const tail = fns.slice(2);

  tail.unshift(input => head(next(input)));


  return composeByRecursion(...tail);
}
```
