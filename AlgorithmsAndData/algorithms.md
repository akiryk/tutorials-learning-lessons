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
