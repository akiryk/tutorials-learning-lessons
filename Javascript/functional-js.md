### Compose
Basic compose function with reduce
```javascript
function compose(...fns) {
  return fns.reduce((a, c) => {
    return v => a(c(v));
  }, v => v)
}

```
Compose with recursion
```javascript
function compose(...fns) {
  if (fns.length === 0) {
    return identity => identity;
  }
  
  if (fns.length === 1) {
    return value => fns[0](value);
  }
  
  const [first, second, ...rest] = fns;
   
  return compose(value => first(second(value)), ...rest);
}

```
