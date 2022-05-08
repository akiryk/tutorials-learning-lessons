# Data Structures

## LinkedIn Learning Course: Programming Foundations, Data Structures

### Numerical types in Java

Whole numbers: int, short, long
Decimals: double, float
Float is more performant, but gives a smaller range.

When we say a language represents `int` values with 32 bits, we mean that every <code>int</code> will have 32 1s and 0s. For example:
<code>00000000000000000000000000000011</code> represents 3. In Java, a double is 64 bits.

### Search types

**Linear Search** is a linear time algorithm. The time it takes increases with the size of the input. A list that's 5 times longer than another will take 5 times longer to search. 

**Big O Notation**
Constant time: O(1)
This means it always takes the same amount of time. 
Example: Find an element by index. It doesn't matter if the array has a million items, you always find it directly with the index.

Linear Time: O(n)
The amount of time increases with the lenth of the list. 

**Why use an array as your data structure**
If you plan on inserting once and then accessing a lot, arrays are a good choice.  

### Linked List
A linked list is comprised of "nodes". Each `node` has a `next` pointer that points to the next node. 

The first node is called the "Head". The last node is called the "Tail", and points to `null`.

Link lists have several actions to **add**, **access**, **delete**, **search**, and **insert info** the list.
