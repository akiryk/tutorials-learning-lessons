# Javascript Tips & Tricks

- Copying an object without mutating it
- Async await

## Optional Chaining
```js
// find array value
const id = response?.data?.employees?.[0]?.name;
```

## Conditionals
```js
// Set value to baz ONLY if foo or bar is true
const myValue = foo || bar ? baz : null;
```

## Create an array

## of n sequential numbers
```js
const myArray = Array.from(Array(10).keys());
// myArray is now [0,1,2,3,4,5,6,7,8,9]

// If you do this, it fills the new array with n copies of the *same* array
Array.from(Array(10).fill([]));
```

## of n arbitrary elements
The above approach won't work for these examples because the above will fill the array with the same object
```js
const arrayOfArrays = new Array(10).fill().map(()=>[]);
// [[], [], [], ...]
const arrayOfObjects = new Array(10).fill().map((e,i)=>({id:i}));
// [{id: 0}, {id: 1}, {id: 2}, {id: 3}, ...];
```

## Copy an object

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

## Async Await

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

## Async Await in an array map

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
