### Compose
Basic compose function with reduce
```javascript
function compose(...fns) {
  return (arg) => fns.reduceRight((result, func)=> func(result), arg)
}

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

Here's a good start for testing:
```javascript
const add = (x, y) => x + y;
const mult = (x, y) => x * y;
const sub = (x, y) => x - y;
const div = (x, y) =>  x / y;

const add10 = (x) => add(x, 10);
const add100 = (x) => add(x, 100);
const add5 = (x) => add(x, 5);
const mult2 = (x) => mult(x, 2);
const mult10 = (x) => mult(x, 10);
const sub2 = (x) => sub(x, 2);
const div2 = (x) => div(x, 2);

```
