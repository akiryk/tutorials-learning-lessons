# Data Structure & Algorithms 

It's important to distinguish these two things. A data structure is used to organize information so it can be processed by an algorithm. We choose the data structure to fit our needs — do we need to do a lot of inserting and deleting? Searching? Priority-management? These will determine the best data structure. 

These notes are from a few sources:
- [Programming Foundations, Data Structures](https://www.linkedin.com/learning/programming-foundations-data-structures)
- [Programing Foundations: Algorithms](https://www.linkedin.com/learning/programming-foundations-algorithms)
- [Primogen's Last Algos Course](https://frontendmasters.com/courses/algorithms/arrays-vs-linked-list/)

## Short cut to quizes
[Linked Lists, Java](https://www.linkedin.com/learning/programming-foundations-data-structures-2/quiz/urn:li:learningApiAssessment:38217226?autoplay=true&resume=false&u=85880466)
[Stacks and Queues](https://www.linkedin.com/learning/programming-foundations-data-structures-2/quiz/urn:li:learningApiAssessment:38215986?autoplay=true&resume=false&u=85880466)
[Hash Tables Quiz](https://www.linkedin.com/learning/programming-foundations-data-structures-2/quiz/urn:li:learningApiAssessment:38219100?autoSkip=true&autoplay=true&resume=false&u=85880466)
[Common Data Structures](https://www.linkedin.com/learning/programming-foundations-algorithms/quiz/urn:li:learningApiAssessment:9897115?autoplay=true&resume=false&u=85880466)

What makes an algorithm efficient? 
The scenario (such as sort this list) and available data structure types (such as an array).

## Search types

**Linear Search** is a linear time algorithm. The time it takes increases with the size of the input. A list that's 5 times longer than another will take 5 times longer to search. 

**Big O Notation**
Constant time: O(1)
This means it always takes the same amount of time. 
Example: Find an element by index. It doesn't matter if the array has a million items, you always find it directly with the index.

Linear Time: O(n)
The amount of time increases with the lenth of the list. 

O of log n time, O(log N): means time goes up linearly while the n goes up exponentially. If it takes 1 second to compute 10 elements, it will take 2 seconds to compute 100 elements, 3 seconds to compute 1000 elements, and so on.

**Why use an array as your data structure**
If you plan on inserting once and then accessing a lot, arrays are a good choice.  

## Ways to store data

### Linked List
A linked list is comprised of "nodes". Each `node` has a `next` pointer that points to the next node. Doubly linked lists also point backwards.

The first node is called the "Head". The last node is called the "Tail", and points to `null`.

Linked lists have several actions to **add**, **access**, **delete**, **search**, and **insert info** the list.

Big O notation for linked lists varies on the action. For accessing an entry, best case is constant time but worst case is linear time.
Add, delete, and search are all also 0(n), because each potentially requires going through the entire list. 
Insert can be 0(1), assuming we insert to the head and not somewhere internal.

Good: 
- it's easy to add and remove items from either the head or the tail, constant time. 
- when adding/removing from anywhere, there's no need to reorganize the underlying memory that holds the data, unlike with arrays. 

Bad: 
- It can't look up an item quickly by index.
- In order to find an item that isn't the head or tail, it needs to walk the list, so big o of n. 

### Arrays
According to Primogen, an array is technically a way to store data in sequenced locations in memory. The locations will depend on the type of data being stored. If the data is 16kb each, less memory is needed for each element than 32b items. In a true array, you have to state up front the number of spots you want reserved as well as what is being reserved. In JavaScript, when we say we're using an array, we're actually using something that wraps an array. 

When we do something like `jsArray.unShift(value)`, we're changing the length of the array AND moving everthing over one spot. This has performance implications. It also means that we need the wrapper code to create a new array under the hood, a new array with more slots. In practice, JS probably creates arrays that come with a few extra slots just in case — but not tons of extra spots. 

Good:
- You can easily get an element by random access (by an index)

### Queues
First of all, a queue is just a specific implementation of a **linked list**. It is a linked list in which the first-item-in will be the first-item-out. FIFO.  

In Queues, the "head" is the first item in the list. If we want to insert a new item, we add it to the tail. If we want to extract an item, we grab it from the front, the head. 
It's helpful to use the terms _enqueue_ and _dequeue_ rather than _push_ and _pop_, since those have a particular meaning in JavaScript.
```js
/**
 * HEAD              TAIL // enqueue(A)
 * HEAD A            TAIL // enqueue(B)
 * HEAD A->B         TAIL // enqueue(C)
 * HEAD A->B->C      TAIL // dequeue()
 * HEAD B->C         TAIL // dequeue()
 * HEAD C            TAIL // dequeue()
 * HEAD              TAIL
 */
```

Assuming we have a pointer to the head and the tail, it's easy/constant-time to get the first item in and to add a new item. 

**Queue Definition:** Like an array but with FIFO behavior only. Unlike an array, it has specific actions:
`enqueue`, `dequeue`, `peek` and sometimes `search`. 

**Queues are good for:** FIFO behavior. Say we're doing some kind of video download buffering and want to asynchronously request data and ensure we send it down in the order it was requested rather than the order it was returned. We could keep track of our requests in a queue using FIFO. 
Dequeuing: Once the request returns, we return that data from the list and move to the next item. 
Enqueueing: If we have another request, we add it to the tail. 

**Bad** Not good for searching or for retrieving an item that isn't at the head or tail. It can be O(n) time for these operations. 

### Stacks

In both Stacks and Queues, the "head" is the item that will be returned first. "Peek()" will display informationa about the head.

**Stack Definition:** A list with LIFO behavior. It generally has these actions:
`push`, `pop`, `peek` (show the head of the list) and sometimes `search`.

**Stacks are good for:** Stacks are great to keeping track of state or the order of when things have occurred. There is no indexing in stacks; if you want to access the next item, you must first pop off the element that's currently at the top of the stack. They are also good for anything where you want to rewind a sequence of events, e.g. with error handling.

**Queue Definition:** Like an array but with FIFO behavior only. Unlike an array, it has specific actions:
`enqueue`, `dequeue`, `peek` and sometimes `search`. 

**Queues are good for:** when things need to happen.

Neither is particularly good for searching or for retrieving an item that isn't at the top (of the stack) or the bottom (of the queue). It can be O(n) time for these operations. 

### Hash Tables

A **hash table** is an form of an **associative array** — a collection of key:value pairs in which order isn't important. We use the terms "put", "add", or "insert", depending on language, for adding a new key/value pair to the table. We always add in pairs. A hash table is very much like a dictionary; the difference is that a hash table requires  applying a hash function to a key and mapping that to a bucket.

**Hashing** A way to mix together some raw data to form a smaller, single piece of data. The process of converting the raw values into the hash a _hash function_.

A major benefit of hash functions is that they are one-way — not reversable.

**How they work** 
Take the starting data, say a string like "PASSWORD", and do something to each character — say, convert it to its ASCII value, 174,324,19, etc. That would be extremely simple, but it's the general idea.

Some terms:
`collision`: When two pieces of data result in the same hash value, we call it a "collision."
`bucket`: the place where the value of the key is stored

This process is _not_ like encryption, because in hashing there isn't a way to decrypt the encoded value. 

In programming, we often use hashing to get to or to store a value at a certain location.


In Java, every object has a `hashCode` function that will return an int. The object's hash value in any language is often based on its underlying `ID` or memory address. 
In JavaScript, you need to import an npm package like slashjs for hash functionality.

**Good**: Fast for retrieving values, but take up more space. Hash map operations are O(1), they always take the same amount of time irrespective of the size of the table. Search, insertion, and deletion all take constant time. 
**Bad**: Don't order their entries; if the data set is small, an array is often more efficient. Collisions can impact performance if there are a lot of them.

## Sets
- A collection of unique items
- order doesn't matter

In JavaScript, you can make a set from an array to remove duplicates (although not duplicate objects unless they are truly the same).

Use a set because:
- you want to eliminate duplication 
- you want to be able to quickly check if a collection contains a particular value. Using `mySet.has(someValue)` is generally faster than `someArray.includes(someValue)`.

```js
const j = {
  name: "Jay",
  id: 1
}

const arr = [
  {
    name: "Phil",
    id: 3
  },
  {
    name: "Phil",
    id: 3
  },
  j,
  j,
]

const mySet = new Set(a);
// mySet will have the two "Phil" objects, but just one j.
```

## Trees
A tree can be thought of as a relative to the linked list; unlike a linked list, tree nodes can each have many nodes.
- A node without parent is called the `root` node.
- A node without children is called a `leaf` node.
- Nodes that share the same parent are called `siblings`

**Binary Search Tree** (BST) has the constraint where each node can only have 2 children. We call them the `left` and `right` nodes. The left is always less and the right always more than the parent, which makes it easy to quickly find a particular value. BSTs are a great way to keep your keys in a sorted order, although they must be kept in balance — i.e. the same number of items on the left as on the right — or they are less efficient. They are often used behind the scenes, as in C++ uses them for implementing sets; Java uses them for TreeMap. 

A balanced tree has a big O of 0(log(N)) because each step removes half of the data for the search. If unbalanced, it bould be up to linear time O(n), because all the data could be on one side of the tree.

**Heaps**
Like a BST but with a much simpler sorting algorithm. Min heaps keep the lowest value on top; max heaps do the opposite. In a min heap, if you start with 10 and then add 20, 10 is the parent of 20 and 20 is the left node. If you then add 30, 30 becomes the right node, and the second child of 10. If you finally add 5, it _would_ become the left child of 20, but it's lesser so it swaps with its parent and again swaps with 10. 
Heaps are often used behind the scenes for priority queues and other structures of programming languages. 

## Recursion
A little quiz:
```py
def countdown(n):
  if (n == 0):
    return n
  else:
    print("count is ", n)
    countdown(n - 1)
    print("over...", n)

countdown(3);
# count is 3
# count is 2
# count is 1
# then what, if anything?
```
## Bubble sort
Starting at the beginning of a list, compare each value with the value to its right and swap positions if it's greater. Then loop again and again, each time stopping 1 short of the previous iteration. E.g. `5, 1, 9, 6, 3` after first run is `1, 5, 6, 3, 9` then `1, 5, 3, 6, 9` then `1, 3, 5, 6, 9`
Not useful because big O is quadratic time of O(n*n), but useful for learning.
It generally has a for loop inside a for loop or inside a while loop. 
```py
def bubbleSort(nums):
  x = len(nums)
  while(x > 1):
    for i in range(0, x - 1):
      current = nums[i]
      next = nums[i+1]
      if (current > next):
        nums[i] = next
        nums[i+1] = current
    x=x-1
  return nums
```
