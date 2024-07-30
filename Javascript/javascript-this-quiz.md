# This in JavaScript

## Quiz
Run the following in jsbin or whatever
```js
bar: function() {
    const x = () => this;
    const y = x();
    if (y === window) {
      console.log('window')
    } else {
      console.log('not window')
    }
  },
  foo() {
    function getThis() {
      return this;
    }
    const x = getThis();
    if (x === window) {
      console.log('window')
    } else {
      console.log('not window')
    }
  }

// What will return
obj.runFunction();

// True of False
const getValueOfX = obj.bar();
console.log(getValueOfX() === obj);
console.log(getValueOfX() === window);

// True of False
const getValueOfX2 = obj.bar;
console.log(getValueOfX2()() === obj);
console.log(getValueOfX2()() === window);
```

