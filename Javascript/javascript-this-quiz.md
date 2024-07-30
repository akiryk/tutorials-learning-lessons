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
  },
  baz() {
    // test with const getValueOfBaz = obj.baz;
    // then see what you get with getValueOfBaz()
    const x = () => this;
    return x;
  }
}

// What will return
obj.runFunction();

getValueOfBaz = obj.baz;
// console.log(getValueOfBaz() === obj) ??
```

