### Compose
Basic compose function with reduce
```javascript
function compose(...fns) {
  return fns.reduce((a, c) => {
    return v => a(c(v));
  })
}
```
Compose with recursion
```javascript
function composer(...fns) {
  if (fns.length === 0) {
    return identity => identity;
  }
  
  if (fns.length === 1) {
    return value => fns[0](value);
  }
  
  const head = fns[0];
  const rest = fns.slice(1);
  const res = [value => head(value), ...rest];
  return compose(...res);
}
```
