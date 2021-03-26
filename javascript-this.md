# This in JavaScript

## Quiz
Run the following in jsbin or whatever
```js
const obj = {
  outerThis: this,
  runFunction: function() {
    console.log(obj.outerThis === this)
  },
  runArrowFunction: () => {
    console.log(obj.outerThis === this)
  },
  whatIsOuterThis: function(){
    console.log(obj.outerThis === window)
    console.log(obj.outerThis === obj)
  },
  whatIsThis: function(){
    console.log(this === window);
    console.log(this === obj);
  },
  whatIsThisArrow: () => {
    console.log(this === window)
    console.log(this === obj);
  }
}

// True or False?
obj.runFunction();

// True or False?
obj.runArrowFunction();

// True or False?
obj.whatIsOuterThis();

// True or False?
obj.whatIsThis();

// True or False?
obj.whatIsThisArrow();
```
