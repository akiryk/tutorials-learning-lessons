# Javascript Tips & Tricks

- Copying an object without mutating it
- Async await

## Deep dive into keyboard events
https://www.youtube.com/watch?v=jLqTXkFtEH0



## Conditionals
```js
// Set value to baz ONLY if foo or bar is true
const myValue = foo || bar ? baz : null;
```

## Array

### Array destructuring
```js
const letters = ['a', 'b', 'c', 'x', 'y', 'z']
const swappedEnds = [letters[0], letters[letters.length - 1]] = [letters[letters.length - 1], letters[0]];
console.log(swappedEnds);
// ['z', 'a']

const swappedArbitrary = [letters[1], letters[3]] = [letters[3], letters[1]];
console.log(swappedArbitrary);
// ["x", "b"]
```
### Array.some() and Boolean function
In javascript, `Boolean` is a function. Who knew? You can use it like this:
```js
const x = [];
Boolean(x.length); // false
Boolean(x.length === 0]); // true
```
It makes a handy way to work with `Array.some()` and the like
```js
const {name, content} = formData; // imagine we can extract these fields from the data;
const fieldErrors = {
   name: validateNameField(name), // returns a string with error message
   content: validateContentField(content),
}
// Now, check if either of the fieldErrors are truthy!
if (Object.values(fieldErrors).some(Boolean)) {
  return badRequest({ fieldErrors, fields });
}

const arrOfObjects = [{id: 1}, {id: 33}, null, {id: 32}];
arrayOfObjects.filter(Boolean);
// [{id: 1}, {id: 33}, {id: 32}];
```

### of n sequential numbers
```js
const myArray = Array.from(Array(10).keys());
// myArray is now [0,1,2,3,4,5,6,7,8,9]

// If you do this, it fills the new array with n copies of the *same* array
Array.from(Array(10).fill([]));
```

### Fill()
Fill() is required to make the array enumarable. `new Array(10)` gives an array that has length of 10, but that's all. You can't map over it.


### of n arbitrary elements
The above approach won't work for these examples because the above will fill the array with the same object
```js
const arrayOfArrays = new Array(10).fill().map(()=>[]);
// [[], [], [], ...]
const arrayOfObjects = new Array(10).fill().map((e,i)=>({id:i}));
// [{id: 0}, {id: 1}, {id: 2}, {id: 3}, ...];
```

## Object

### Key/Value hashes
Spread an array into an object to create a key/value hash
```js
const colors = ['red', 'blue', 'green'];
const map = {...colors};
/*
{
  0: 'red',
  1: 'blue',
  2: 'green'
}
*/
```

Use `Object.fromEntries()` to transform key/value pairs into an object
```js
const jobs = [["Phil", "Baker"],["Scott", "Dancer"], ["Ellen", "Trainer"]];
Object.fromEntries(jobs);
/*
{
  Ellen: "Trainer",
  Phil: "Baker",
  Scott: "Dancer"
}
*/
```


### Optional Chaining
```js
// find array value
const id = response?.data?.employees?.[0]?.name;
```

### Copy an object

Say we have an object with deeply nested data, and we want to make a copy that only changes one of the deeply nested properties.
```js
const data = {
    page: {
      card: {
        cardType: {
          typeA: {
            cardTypeAData: {
              name: "Card Type A",
              id: 1,
              color: "blue", // we want to change this to "red"
             }
           }
         }
      }
   }
}

```

Use spread operator to destructure each property all the way down:
```js
 const copy = {
    ...data,
    page: {
        ...data.page,
        card: {
            ...data.page.card,
            cardType: {
                ...data.page.card.cardType,
                typeA: {
                    ...data.page.card.cardType.typeA,
                    cardTypeAData: {
                        ...data.page.card.cardType.typeA.cardTypeAData,
                        color: "red",
                    }
                }
            }
        }
    }
}
```

## Async 

### Async Await

```js
// Imagine getUsers returns a promise; put the `async` keyword immediately before the function.
const getUsers = async () => {
    try {
        const users = await callToEndpoint.getUsers();
        // next line won't execute until the request returns:
        doSomethingWithData(users);
    } catch(error) {
        console.log(error.message);
    }
} 
```

### Async Await in an array map

- Say you have a 2d array -- an array that holds arrays of IDs.
- You want to load data by ID for each of the IDs
- Loading the data is asyncronous, so you need a way to iterate over `x` number of arrays and asyncronously load `y` number of items.

```js
// assume an array of arrays of IDs like so:
const arrayOfIds = [['ID1', 'ID2', 'ID3'], ['ID1', 'ID4'], ['ID2', 'ID3', 'ID5']];

// This function will iterate over the array of arrays, and resolve all of the promises before proceeding.
const getAsyncDataInArrays = async (outerArray) => {
  const data = await Promise.all(
    outerArray.map(async innerArray => await Promise.all(
        innerArray.map(async id => await getAsyncDataById(id))
    ))
  )
  console.log(data)
}

function getAsyncDataById(id) {
  return new Promise((resolve, reject) => {
     window.setTimeout(() => {
       switch(id) {
        case 'ID1': 
           return resolve({
             id: 1,
             name: "Red"
           });
           break;
        case 'ID2':
           resolve({
             id: 2,
             name: "Blue"
           });
           break;
        case 'ID3': 
          resolve({
             id: 3,
             name: "Green"
          });
          break;
        case 'ID4': 
            resolve({
             id: 4,
             name: "Yellow"
           });
           break;
         default:  resolve({
             id: 5,
             name: "Orange"
           });
      }
    }, 10)
  });
}

// Now, if we call the function
getAsyncDataInArrays(arrayOfIds);

// We get output like so:
[
  [
    { id: 1, name: "Red" },
    { id: 2, name: "Blue" },
    { id: 3, name: "Green" },
  ],
  [
    { id: 1, name: "Red" }, 
    { id: 4, name: "Yellow" }
  ], // etc
```
