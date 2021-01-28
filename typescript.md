# Typescript

## Resources
* [FrontEnd Masters Typescript](https://frontendmasters.com/courses/typescript-v2) course. 
* [Github repo](https://github.com/mike-works/typescript-fundamentals)
* [Course Notes](https://mike.works/course/typescript-fundamentals-7832c19)
* [Course Slides](https://docs.mike.works/typescript-slides-v2)

## Why?

* Encode constraints and assumptions of the developer
* Catch comment mistakes (e.g. spelling errors)
* Find some errors at compile time
* Provide a better developer experience

## Get Started

* Clone the repo and `yarn`
* `npx tsc` to install typescript compiler

## Configure
Create a `tsconfig.json` file to configure target JS version, output directory, etc:
```json
{
  "compilerOptions": {
    "jsx": "react",
    "strict": true,
    "noImplicitAny": true,
    "module": "commonjs",
    "target": "ES2017",
    "outDir": "lib",
    "declaration": true,
    "sourceMap": true
  },
  "include": ["src"]
}
```
The above will create your ts files in `lib/` folder and will compile them to work with ES2017.
* declaration enables VSCode to understand and help debug ts files (ie. it create a type declaration file)
* noImplicitAny: wildcards, where any type is allowed -- good to prohibit
* jsx enables jsx

## Basics

See the [course notes for basics.ts](https://github.com/mike-works/typescript-fundamentals/blob/master/notes/1-basics.ts)

### Variables
Some variables can be typed by inference:
```js
// The jsdocs notation will be undestood by Typescript:
/**
 * x is a string!
 */
let x = "hello world";
// x is a string by inference; the comment is from jsdocs:
x = 32; // ERROR, if you hover over `x`, you'll see, "x is a string!"

// Any type!
let z; // z is assigned `any`
z = 41;
z = "abc"; // No error or alert!

// Type annotation
let z: number;
z = 31; // fine
z = "hi there"; // ERROR Type '"abc"' is not assignable to type 'number'.

```

### Arrays 
```js
let aa: number[] = [];
aa.push(33);
aa.push("abc"); // 🚨 ERROR: Argument of type '"abc"' is not assignable to parameter of type 'number'.

// an array of "nevers"; it will never work
let aa = [];
aa.push(33); // ERROR

// "Tupple" an array of fixed length; follows a convention
```

### Objects
```js
//== OBJECTS ==//

/**
 * (11) object types can be expressed using {} and property names
 */
let cc: { houseNumber: number; streetName: string };
cc = {
   streetName: "Fake Street",
   houseNumber: 123
};

cc = {
   houseNumber: 33
};
/**
 * 🚨 Property 'streetName'
 * 🚨   is missing in type   '{ houseNumber: number; }'
 * 🚨   but required in type '{ houseNumber: number; streetName: string; }'.
 */
 
 // if we want to re-use this type, we can create an interface
interface Address {
  houseNumber: number;
  streetName?: string; // streetName is optional (?:)
}
// and refer to it by name
let ee: Address = { houseNumber: 33 };

```

### Interaction & Union Operators
Intersection ('OR'), is `|`
Untion ('AND'), is `&`

### Structural vs Nominal Typing
Typescript is a `structural` type system — it only cares about the *shape* of an object. A car type is a car type if it has `make`, `model`, `year`, that are strong, string, and number.  

Taking this approach can help V8 optimize your JavaScript.

### Wide vs Narrow Types
The widest is `any`; it can take anything.
An array of any is narrower.
A string is narrow.

## Function Basics

See notes about [functions from course](https://github.com/mike-works/typescript-fundamentals/blob/master/notes/2-function-basics.ts)

In functions, return types can almost always be inferred; however it is usually safer to be explicit. There can be unintended consequences to what the infered values will be. 

Rest params need to be array since that's what rest params are: 

`const sum = (...vals: number[]) => vals.reduce((sum, x) => sum + x, 0);`

### Overload functions
If you overload a function, you can provide explicit rules given different dependencies:
```js
interface HasPhoneNumber {
  name: string;
  phone: number;
}

interface HasEmail {
  name: string;
  email: string;
}

// "overload signatures"
function contactPeople(method: "email", ...people: HasEmail[]): void;
function contactPeople(method: "phone", ...people: HasPhoneNumber[]): void;
// If you use "email", you must provide people as a HasEmail interface type.

// "function implementation"
function contactPeople(
  method: "email" | "phone",
  ...people: (HasEmail | HasPhoneNumber)[]
): void {
  if (method === "email") {
    // as is a typescript operator, not vanilla JS
    (people as HasEmail[]).forEach(sendEmail);
  } else {
    (people as HasPhoneNumber[]).forEach(sendTextMessage);
  }
}
```

### Lexical Scoping
Lexical scoping concerns the value of `this`. If you need to pass `this`, see the [lexical scoping section](https://github.com/mike-works/typescript-fundamentals/blob/master/notes/2-function-basics.ts) of the notes.

## Type Aliases and Interfaces
These are both ways to give a name to a structure we can import and export. 
Type aliases are eager; interfaces are lazy.

### Type Aliases
Just a way to give a type a name:

`type EmailOrPhone = string | number;` or

`type hasName = { name: string }

```js
// this enables us to replace this with the following:
const x: string | number;
const y: EmailOrPhone;
```
### Interfaces
While aliases can handle any type — primitives likes string as well as object or array — interfaces can **only** handle objects or arrays or functions (things that have `prototypes`)

Interface and alias can do the same thing:

```js
// note return type void using colon
interface ContactMessenger1 {
  (contact: HasEmail | HasPhoneNumber, message: string): void;
}

// for alias, it must us fat arrow
type ContactMessenger2 = (
  contact: HasEmail | HasPhoneNumber,
  message: string
) => void;
```

