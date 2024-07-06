# Challenges

### 1. Create a function that returns n arrays of arbitrary length and that contain arbitrary initial data. 
```js
// example
const setValues = () => ({
   value: '',
   state: 'INITIAL'
});
const arrays = initialize2DArray({
  lengthOfFirstDimension: 3,
  lengthOfSecondDimension: 5
}, setValues);

console.log(arrays)

[
  [
    { value: '', state: 'INITIAL' },
    { value: '', state: 'INITIAL' },
    { value: '', state: 'INITIAL' },
  ],
  [
    { value: '', state: 'INITIAL' },
    { value: '', state: 'INITIAL' },
    { value: '', state: 'INITIAL' },
  ],
  [
    { value: '', state: 'INITIAL' },
    { value: '', state: 'INITIAL' },
    { value: '', state: 'INITIAL' },
  ],
]
