# This in JavaScript

## Quiz
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
  whatIsThis: function(){
    if (this === window) {
      console.log("this is window in fn")
    } else if (this === obj) {
      console.log('this is obj in fn')
    }
  },
  whatIsThisArrow: () => {
    if (this === window) {
      console.log("this is window in arrow fn")
    } else if (this === obj) {
      console.log('this is obj in arrow fn')
    }
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
