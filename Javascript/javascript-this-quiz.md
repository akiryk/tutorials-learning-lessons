# This in JavaScript

## Quiz

document.addEventListener('click', () => {
  console.log(this); // what is this?
})

document.addEventListener('click', function() {
  console.log(this); // what is this?
})

Run the following in jsbin or whatever
```js
const obj = {
  outerThis: this,
  runFunction: function() {
    if (obj.outerThis === this){
      console.log('outerThis === this in function')
    } else {
      console.log('outerThis !== this in function')
    }
  },
  runArrowFunction: () => {
    if (obj.outerThis === this){
      console.log('outerThis === this in arrow fn')
    } else {
      console.log('outerThis !== this in affor fn')
    }
  },
  whatIsOuterThis: function(){
    if (obj.outerThis === window) {
      console.log("outerThis is window")
    } else if (obj.outerThis === obj) {
      console.log('outerThis is obj')
    }
  },
  whatIsThisArrow: () => {
    if (this === window) {
      console.log("this is window in arrow fn")
    } else if (this === obj) {
      console.log('this is obj in arrow fn')
    }
  },
  bar: function() {
    const x = () => this;
    const y = x();
    if (y === window) {
      console.log('window')
    } else {
      console.log('obj')
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
      console.log('obj')
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

