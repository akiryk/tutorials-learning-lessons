# LinkedIn Learning Course: Programming Foundations, Data Structures

## Short cut to quizes
[Linked Lists, Java](https://www.linkedin.com/learning/programming-foundations-data-structures-2/quiz/urn:li:learningApiAssessment:38217226?autoplay=true&resume=false&u=85880466)
[Stacks and Queues](https://www.linkedin.com/learning/programming-foundations-data-structures-2/quiz/urn:li:learningApiAssessment:38215986?autoplay=true&resume=false&u=85880466)
[Hash Tables Quiz](https://www.linkedin.com/learning/programming-foundations-data-structures-2/quiz/urn:li:learningApiAssessment:38219100?autoSkip=true&autoplay=true&resume=false&u=85880466)

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

### Stacks and Queues

In both Stacks and Queues, the "head" is the item that will be returned first. "Peek()" will display informationa about the head.

**Stack Definition:** A list with LIFO behavior. It generally has these actions:
`push`, `pop`, `peek` (show the head of the list) and sometimes `search`.

**Stacks are good for:** Stacks are great to keeping track of state or the order of when things have occurred. There is no indexing in stacks; if you want to access the next item, you must first pop off the element that's currently at the top of the stack. They are also good for anything where you want to rewind a sequence of events, e.g. with error handling.

**Queue Definition:** Like an array but with FIFO behavior only. Unlike an array, it has specific actions:
`enqueue`, `dequeue`, `peek` and sometimes `search`. 

**Queues are good for:** when things need to happen.

Neither is particularly good for searching or for retrieving an item that isn't at the top (of the stack) or the bottom (of the queue). It can be O(n) time for these operations. 

### Hash Based Data Structures

**Associative Array** a collection of key:value pairs, order isn't important.

**Hashing** A way to mix together some raw data to form a smaller, single piece of data. The process of converting the raw values into the hash a _hash function_.

A major benefit of hash functions is that they are one-way — not reversable.

**How they work** 
Take the starting data, say a string like "PASSWORD", and do something to each character — say, convert it to its ASCII value, 174,324,19, etc. That would be extremely simple, but it's the general idea.

Some terms:
`collision`: When two pieces of data result in the same hash value, we call it a "collision."
`bucket`: the place where the value of the key is stored

This process is _not_ like encryption, because in hashing there isn't a way to decrypt the encoded value. 

In programming, we often use hashing to get to or to store a value at a certain location.

A **hash table** is an implementation of the associative array data structure. We use the terms "put", "add", or "insert", depending on language, for adding a new key/value pair to the table. We always add in pairs. A hash table is very much like a dictionary; the difference is that a hash table requires  applying a hash function to a key and mapping that to a bucket.

In Java, every object has a `hashCode` function that will return an int. The object's hash value in any language is often based on its underlying `ID` or memory address. 
In JavaScript, you need to import an npm package like slashjs for hash functionality.

**Pros/Cons** 
Fast for retrieving values, but take up more space. Hash map operations are O(1), they always take the same amount of time irrespective of the size of the table. Search, insertion, and deletion all take constant time. The caveat is if you have collisions and must implement linked list in your buckets.
