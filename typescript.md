# Typescript

Skip to the bottom to see random examples

## Resources
* [FrontEnd Masters Typescript](https://frontendmasters.com/courses/typescript-v2) course. 
* [Github repo](https://github.com/mike-works/typescript-fundamentals)
* [Course Notes](https://mike.works/course/typescript-fundamentals-7832c19)
* [Course Slides](https://docs.mike.works/typescript-slides-v2)
* [DTS Lint](https://github.com/Microsoft/dtslint) - a good resource for testing that your types get what they expect and error correctly
* [Typescript Playground](https://www.typescriptlang.org/play)

## Quiz Show Course
### Variadic Tuples
Example tuple could be a color. A color has RGB values, so it might look like this: `[[r: 123], [g: 34], [b: 233]]`

Before TS4, we had to do this:
```js
// MyTyple is an array of a number followed by any number of elements of type T
type MyTuple<T> = [number, ...T[]]

const x1:MyTuple<string> = [4, "cat", "dog", "bear"]; // this works
const y:MyTuple<Array<number>> = [44, [1,2,4,3,6]]; // also works!
const z:MyTuple<Array<number>> = [44, 2,3,4,5]; // no, can't assign numbers to this type

// We can now do stuff like this:
type Pork = [
    ...[number, number],
    ...[string, string, string]
]

const p:Pork = [3, 4, 'red', 'blue', 'yelllow']; // yes
const p1:Pork = [3,4, 'red', 'blue']; // no!

// you can use rest anywhere:
type Salmon = [string, ...number[], string];
const s:Salmon = ['red', 4, 5, 6, 'blue']; // yes!
```
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

// array of objects (see below for example of an object type)
const contacts: contactType[] = [];

// "Tupple" an array of fixed length; follows a convention
```

### Objects
```js
// required and optional types:
type contactType = { houseNumber: number; streetName: string, apt?: string };
const myContact: contactType = {
   streetName: "Fake Street",
   houseNumber: 123
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

### Personal Note
While Interfaces seem to give more power, by being extensible, that might actually not be a good thing. It means you could have more than one interface with the same name; overloading can be difficult for other devs to follow. Type aliases can do the same things and may be a better option.

This is a useful [StackOverview](https://stackoverflow.com/questions/41682572/when-to-use-types-vs-interface-in-ts/41683135#41683135) of types vs. interfaces

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

Interface and alias can do the same things, except that Interfaces can't handle primitives and aliaes can't extend. This could be an argument in favor of using Aliases, since they avoid the confusion/complications of extending interfaces and using the same name multiple times. 

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

Note that you can declare an interface more than once — that is, you can narrow it:

```js
interface PhoneNumberDict {
  // arr[0],  foo['myProp']
  [numberName: string]:
    | undefined
    | {
        areaCode: number;
        num: number;
      };
}

// we declare it again, this time narrowing it to require a home and an office key
interface PhoneNumberDict {
  home: {
    /**
     * (7) interfaces are "open", meaning any declarations of the
     * -   same name are merged
     */
    areaCode: number;
    num: number;
  };
  office: {
    areaCode: number;
    num: number;
  };
}
```

## Classes

### Definite Assignment Operator
Add exclamation mark to tell Typescript to not throw an error the way it ordinarily would; let you handle it. For example:
```js
private password!: string 
// now even though no password is passed in,  you are saying that you'll create one and it will be a string
```

## Converting Javascript to Typescript
You can have `.js` and `.ts` modules side by side. You can import one from the other. It's not like changing from one programming language to another. 
### What not to do
- Don't make functional changes at the same time. If you check that something is falsy now, don't change to checking if it's undefined with TypeScript.
- Don't neglect to write tests for your types — use dtslint for type tests
### Three step process js to ts
**PR 1: Compile in "Loose Mode"**
  - Tests should pass
  - Rename all .js files to .ts
  - change tsconfig.json as below
  - Fix only things that are not type-checking, or causing compile errors
  - don't change behavior
  - don't run `tsc src/index.ts` or the like -- don't convert at this point
  - Make sure tests are still passing and submit your PR!
  
```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": false
  }
}
```
  
**PR 2: Explicit any**
  - tests pass
  - ban implicit `any`
  - where possible provide a specific type
      - use [Definitely Typed](https://github.com/DefinitelyTyped/DefinitelyTyped) package to convert untyped libraries like Lodash to use types  
```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": true
  }
}
```
      
**PR 3: Squash Explicity any and enable strict mode**
```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": true,
    "strict": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictBindCallApply": true
  }
}
```
Also, try really hard to avoid casting with `as` keyword, where you force TypeScript to regard something as a particular type.

## Random Examples
```tsx
type LoaderData = {
  // this is a handy way to say: "posts is whatever type getPosts resolves to"
  posts: Awaited<ReturnType<typeof getPosts>>;
};
```

## Arrays
There are two ways to type arrays. For an array of numbers, for example:

1. Generic: `Array<number>` 
2. Shorthand: `number[]`

These are equivalent.
