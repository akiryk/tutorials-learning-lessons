# Performance

Terms
* SLO: service level objective

## FEM Course

### JavaScript performance

* When you run Chrome performance tab and see the Summary chart, the yellow part is called "scripting." This is the compilation step and often represents the largest portion of time.

* Use the User Timing API to find the biggest problems

* Type systems help because V8 optimizes based on whether it sees the same types of objects under the same conditions. 

Using the timing API:
```js
const { performance } = require('perf_hooks');

let iterations = 1000000;
const square = (x) => x * x;
const sumOfSquares = (a, b) => square(a) + square(b);

performance.mark('start');

while (iterations--) {
  sumOfSquares(iterations, iterations + 1);
}

performance.mark('end');
performance.measure('my measure', 'start', 'end');
const [measure] = performance.getEntriesByName('my measure');
console.log(measure);
```
