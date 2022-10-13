### Basic compose function with reduce
```javascript
function compose(...fns) {
  return fns.reduce((a, c) => {
    return v => a(c(v));
  })
}
```
