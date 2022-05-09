# LinkedIn Learning Course: Programming Foundations, Data Structures

## Numerical types in Java

Whole numbers: int, short, long
Decimals: double, float
Float is more performant, but gives a smaller range.

When we say a language represents `int` values with 32 bits, we mean that every <code>int</code> will have 32 1s and 0s. For example:
<code>00000000000000000000000000000011</code> represents 3. In Java, a double is 64 bits.

## Search types

**Linear Search** is a linear time algorithm. The time it takes increases with the size of the input. A list that's 5 times longer than another will take 5 times longer to search. 

**Big O Notation**
Constant time: O(1)
This means it always takes the same amount of time. 
Example: Find an element by index. It doesn't matter if the array has a million items, you always find it directly with the index.

Linear Time: O(n)
The amount of time increases with the lenth of the list. 

**Why use an array as your data structure**
If you plan on inserting once and then accessing a lot, arrays are a good choice.  

## Ways to store data

### Linked List
A linked list is comprised of "nodes". Each `node` has a `next` pointer that points to the next node. 

The first node is called the "Head". The last node is called the "Tail", and points to `null`.

Linked lists have several actions to **add**, **access**, **delete**, **search**, and **insert info** the list.

Big O notation for linked lists varies on the action. For accessing an entry, best case is constant time but worst case is linear time.
Add, delete, and search are all also 0(n), because each potentially requires going through the entire list. 
Insert can be 0(1), assuming we insert to the head and not somewhere internal.

### Stack
**Definition:** Like an array but with LIFO behavior only -- i.e. an array with `push` and `pop` behavior only.

**Good for:** Stacks are great to keeping track of state or the order of when things have occurred. There is no indexing in stacks; if you want to access the next item, you must first pop off the element that's currently at the top of the stack. They are also good for anything where you want to rewind a sequence of events, e.g. with error handling.
