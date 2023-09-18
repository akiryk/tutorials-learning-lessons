# Programming Foundations: Algorithms
From [LinkedInLearning](https://www.linkedin.com/learning/programming-foundations-algorithms/)

## Algorithm Characteristics

### Complexity
**Space Complexity**: memory requirements
**Time Complexity**: time requirements

### Inputs and Outputs
An algorithm accepts certain inputs and outputs certain results.

## Common Algorithms
- Search
- Sort
- Computation: derives a new set of data from an existing set of data?
- collection: manipulate or navigate

## Measuring Performance
We use the term Big O because it refers to "order of operation." In order of complexity:
o(1): constant time
o(log n): logarithmic time
o(n) linear time
o(n log n) log linear time
o(n*n) quadratic time



| Notation | Description | Example | 
| -------- | ----------- | ------- |
| o(1) | Constant Time | Look up an element in array by index |
| o(log n) | Logarithmic Time | Find element in sorted array with binary search |
| o(n) | Linear Time | search an unsorted array for a value | 
| o(n log n) | log linear time | complex sorting like heap sort or merge sort |
| o(n * n) | quadratic time | sorting algorithms like bubble sort, selection sort, etc |

## Binary Search Test 
answers below
```js
const list = [10, 20, 22, 25, 28, 31, 44, 532, 10100];
const needleTrue = 20;
const needleFalse = 4999;
binarySearch(list, needleTrue); // return true!
binarySearch(list, needleFalse); // return false!
```

## Binary Search Answer
```js
const list = [10, 20, 22, 25, 28];

export default function bs_list(haystack: number[], needle: number): boolean {
    let lo = 0;
    let hi = haystack.length;

    do {
        const m = Math.floor(lo + (hi - lo) / 2);
        const v = haystack[m];
        if (v === needle) {
            return true;
        } else if (v > needle) {
            // search to the left!
            hi = m;
        } else {
            lo = m + 1;
        }
    } while (lo < hi);

    return false;
}
```

## Crystal balls question
You have two crystal balls and they will break at a certain height. What algorithm could you use to have better performance than linear or binary search? 

Linear: you could drop the first ball at 1ft, then 2ft, 3ft, etc. Eventually, it will break. This is linear time (o of n)
Search: or you could divide in half, then use linear for the second ball. This doesn't really buy you anything; it's still o of n because we ignore the constants

## Crystal balls answer
If you search for a spot that breaks by jumping in increments of the square root, you'll limit the possible items you check to the sqrt. This means your big-o will be sqrt of n. 
```js
function two_crystal_balls(breaks) {
    const jumpAmount = Math.floor(Math.sqrt(breaks.length));

    let i = jumpAmount;
    
    for (; i < breaks.length; i += jumpAmount) {
         console.log(i)
        if (breaks[i]) {
            break;
        }
    }

    i -= jumpAmount;

    for (let j = 0; j < jumpAmount && i < breaks.length; i++, j++) {
      console.log(i)
        if (breaks[i]) {
            return i;
        }
    }

    return -1;
}

const f = false;
const t = true;

const a = [f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,f,t,t,t,t,t,t,t,t]

two_crystal_balls(a)
```
## Bubble Sort
Start with a list of numbers
Return a sorted list of numbers

## Bubble Sort Answer
Simple: 
- loop through the array and compare each element with its neighbor.
- if the first is larger than the second, then swap.
- after one iteration of this loop, the largest element will be on the far right
- now repeat the loop but make it one element shorter (don't compare the last element)
- and so on

Because this algorithm loops twice, the big o is o of n squared.
Technically, it requires n-squared + n / 2, but we ignore the constants

```js
function bubbleSort(unsortedList) {
  const sorted = [...unsortedList];
  let j = sorted.length - 1;
  while(j > 0) {
    for (let i = 0; i < j; i++) {
      if (list[i] > list[i+1]) {
        // swap them!
        const bigger = list[i];
        list[i] = list[i + 1];
        list[i + 1] = bigger;
      }
    }
    j--;
  }
  return sorted;
}
```
