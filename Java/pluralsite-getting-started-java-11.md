# Getting Started with Programming in Java 11

See https://app.pluralsight.com/library/courses/getting-started-programming-java/table-of-contents

## Create your first app

- Add a package name to give unique namespace: `package com.kiryk.myapp;`
- use the `Main` class
- run from command line by using `java` command from appropriate directory, e.g. `java path/to/dir/com/kiryk/myapp/Main`

## Variables
- Java is strongly typed
- variables can be reassigned
- keyword `final` prevents reassignment

### Primitive data types

Primitive types are assigned by value. It's just like in JavaScript. 
```js
var x = 10; // some space in memory is assigned to x and set to 10
var y = x;  // some space in memory is assigned to y and set to 10
x = 100;    // y is still 10!
```

Integer types:
- int: any number from negative to positive in the 32 bit range
- byte: 8 bits, meaning the only options are -128 to 127.
- short: 16 bits
- long: 64 bits. To use when declaring a literal, you need to add `L`, as in `long x = 4500000000000L;`

Floating types:
- float: 32 bit value. When declaring a literal, you need to add `f`, as in `float x = 4.5342f;`
- double: 64 bit value, no need for `d` but you can add if you want, `double x = 4.0000000000005d` or `double 4.0000000000005`

Char: a single unicode character, `char accentedU = '\u00DA'; // Ú`

Bool: `boolean x = true;`

### Operators
They act pretty much as you'd expect except in the case of division on `int` values. When dividing intigers, `7 / 2` results in `3`, no rounding, just the whole number.

Compound assignment operators: `+=` `-=` `/=`, etc. 

Precedence: 

- multiplicative operators (`*, /, %`) take precedence over additive ones, so `5 + 5 * 5 = 30` not 50.
- When there are more than one type of operator, precedence goes left to right, so `5 * 5 / 5 = 5` not 5.
