# Typescript

## LinkedIn Learning Course

### Setup
When setting up `tsconfig.json`, use the `noEmit: true` prop to tell TS not to create any other files. Do this if you'll use Babel or something else as your compiler. Otherwise, set it false, and TS will output `.js` files where you tell it in the `outDir` directory.

Add `allowJs: true` to allow existing JS files and `checkJs: false` to avoid checking js files. 

Skip to the bottom to see random examples

### Interfaces and Types
```ts
interface Contact {
  name: string,
  phone: number,
  sayHi(name: string): Contact
}

interface Address {
  street: string,
  zipcode: number
}

type FullContact = Contact & Address;

const c: FullContact = {
  name: "Bill",
  phone: 23234234,
  street: "whatever",
  zipcode: 32433
}
```

### Enums 
```ts
// It's often easier to use a Union rather than an enum:
const ERROR = "error";
const ACTIVE = "active";
const INACTIVE = "inactive";

// then reference the pseudo-enums directly:
type Status = "active" | "inactive" | "error";

// Or use the typeof operator:
type Status = typeof ERROR | typeof ACTIVE | typeof INACTIVE;

// Either way:
const myStatusA = "active"; // good!
const myStatusB = ACTIVE;   // good!
const myStatusC = "bergle"; // bad!

// However, if you want an enum, use enum keyword:
enum Status {
    ACTIVE,
    INACTIVE,
    ERROR
}

type Person = {
    status: Status,
    name: string
}

const carl: Person = {
    status: Status.ERROR,
    name: "Carl"
}
```
If you must use strings, do it like this:
```ts
enum Status {
    ACTIVE = "ACTIVE,
    INACTIVE = "INACTIVE",
    ERROR = "ERROR"
}
```

### Generics
```ts
// clone can be called with any type, T, and will return something also of type T.
function clone<T>(source: T): T {
  return source;
}
// note that this doesn't work with arrow functions

// Generic can be used with constraints, e.g. this function takes any type T
// as longs as T is an object with a numeric id property
function getNextID<T extends {id: number}>(todoItems: Array<T>) {
  const id = todoItems[0].id;
}

// Multiple generics are allowed:
function handle<T1, T2>(value: T1): T2 {
  //... something  
}

// call with this syntax
handle<number, string>(500);
    
```

### Advanced Types

QUIZ Challenge: https://www.linkedin.com/learning/typescript-essential-training-14687057/challenge-the-right-type?autoSkip=true&autoplay=true&resume=false&u=85880466

**Keyof** and **Index Acccess Types**
```ts
// Keyof enables you to access each key in a type or interface
type Contact = {
  name: string,
  age: number
}

// assuming getField is called with Contact type:
// keyof T will be "name" and "age"
// T[keyof T] will be string and number
// 
function getField<T>(source: T, property: keyof T): T[keyof T] {
  return source[property]; // index access type, e.g. Contact["name"]
}

const c1: Contact = { // ... a contact }
getField(c1, "name");  // yes!
getField(c1, "email"); // no!

function getId<T extends { id: number} >(thing: T) {
    return thing.id;
}

type Shape = {
    id: number,
    width: number
    name: string
}

type ZooAnimal = {
    id: number
    section: string
}

const box: Shape = {
    id: 1,
    width: 55,
    name: "box"
}

const parrot: ZooAnimal = {
    id: 2,
    section: "jungle"
}

getId(box);    // 1
getId(parrot); // 2

// Index Access Type
// val can be of any of the types in type T. If T is Shape, that means val can be id of number, width of number or name of string
function flexibleFn<T>(val: {
    [TType in keyof T]: T[TType]
}) {
    
}
```

### Utility Types

There are [several utility types](https://www.typescriptlang.org/docs/handbook/utility-types.html), and they are worth using for certain use cases. 

**Record** can map a new type to existing type
```ts
// "string" refers to the key, e.g. id and value. 
// "string | number" refers to the possible values.
type MyRecordType = Record<string, string | number>
const x: MyRecordType = { name: "Bill"}; // fine
x.age = 33; // fine
x.callback = () => return "Bill"; // NO!

type Cell = {
    id: number,
    value?: string
}

const gridCells: Record<string, Cell> = {
    cell0: {
        id: 1,
        value: "A"
    },
     cell1: {
        id: 2,
        value: "B"
    },
     cell2: {
        id: 3,
    },
}
  ```
 **Partial**
 ```ts
 // id, callback, and name are required
 type X = {
   id: number,
   name: string,
   callback: Function
 }
 
 type PartialX = Partial<X>;
 
 // p passes because values are all optional now
 const p = {
   id: 1
 }
```
**Other useful utilities** 
- `Pick`
- `Omit`
- `Require`

## Decorators
Decorators enable you to wrap classes, methods, and properties in functions that enhance or modify behavior. They are a Typescript implementation of a _proposed_ addition to JavaScript, so subject to change.

Examples include:
- decorate a class with `@singleton` to make any class a singleton
- decorate a method with `@authorize` to enable any method to throw an error if user doesn't have correct permissions
- decorate a property with `@auditable` to audit any time the property changes

Note that these decorators and names are all custom and arbitrary. The way they are implemented depends on whether you are decorating a class, method, or property. 

Decorating a **method** is the most straightforward. 

```ts
class Contacts {

  @authorize("Editor"); // getContact should only be accessed by a user with "Editor" permissions
  getContact() {
    // ... do stuff
}

// outside of the class, create the decorator factory
function authorize(roleID: string) {
    /**
     * @param {object} target - the object that the decorator is applied to; e.g. instance of the object that the method belongs to
     * @param {string} property - the name of the property the decorator is applied to
     * @param {object} PropertyDescriptor = an object containing metadata about the property. 
     *   It is the data about whether given object is enumerable, writable, etc. See [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).
     */
    return function authorizeDecorator(target: any, property: string, descriptor: PropertyDescriptor) {
        const wrapped = descriptor.value; 
        descriptor.value = function() {
            if (!currentUser.isAuthenticated()) { throw Error("No auth!") }
            if (!currentUser.isInRole(roleID)) { throw Error(`Not right role, ${roleID}!`) }
            
            return wrapped.apply(this, arguments);
        }
    }
}
```

## Resources
* [FrontEnd Masters Typescript](https://frontendmasters.com/courses/typescript-v2) course. 
* [Github repo](https://github.com/mike-works/typescript-fundamentals)
* [Course Notes](https://mike.works/course/typescript-fundamentals-7832c19)
* [Course Slides](https://docs.mike.works/typescript-slides-v2)
* [DTS Lint](https://github.com/Microsoft/dtslint) - a good resource for testing that your types get what they expect and error correctly
* [Typescript Playground](https://www.typescriptlang.org/play)

## Quiz Show Course

Look through the notes for the different quizes and challenges: https://www.typescript-training.com/course/making-typescript-stick/05-does-it-compile/

### Variadic Tuples
Example tuple could be a color. A color has RGB values, so it might look like this: `[[r: 123], [g: 34], [b: 233]]`

```js
// Before TS4, we had to do this:
// MyTyple is an array comprised of a single number followed by any number of elements of type T
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

### Template Literal Types
```js
type Key = `${number}::${number}`;

type Cells = {
  [key: Key]: number
}

const grid:Cells = {
    "0::0": 3, // yes!
    "0:1": 4, // no!
}
```

This works very well with the new **[key remapping feature](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#key-remapping-via-as)**.

### Checked Index Access
There's a new TS configuration option, `noUncheckedIndexedAccess`, that adds 'undefined' to any undeclared field in the type.
```js
// We have a dictionary comprised of keys and values, in which value is whatever we set it to, T.
type Dict<T> = {[K: string]: T };

// Make an instance of Dictionary in which values are arrays of strings
const d:Dict<string[]> = {};

// declare a field
d.color = ['one', 'two']; // yes!

// try doing something with an undeclared field:
d.size.push('fresh'); // no! 

// solve by adding a guard
if (d.size) { d.size.push('fresh'); } // yes!

// alternate way to handle this is to explicitly add undefined to the type declaration
type Dict<T> = { [K: string]: T | undefined }
```

## Type Guards
Use a conditional block to narrow down the type, [per docs](https://www.typescripttutorial.net/typescript-tutorial/typescript-type-guards/).

- use `typeof` of `instanceof`
- or use a user-defined typeguard with the `is` keyword, as in `arg is someType` 

```ts
class Dog { // we have a class for Dogs }
function getIsTypePet(arg: any): arg is Dog {
  return arg instanceof Dog;
}

// general is undefined check:
function isDefined<T>(arg: T | undefined): arg is T {
   return typeof arg !== "undefined";
}
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

## Handle undefined types
```js
// isDefined takes an argument of type T or undefined
// it returns true if the argument is not undefined. 
// The `is` keyword is part of a type predicate and gives more control than making the return a boolean.
// see: https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates
function isDefined<T>(x: T | undefined): x is T {
  return typeof x !== "undefined";

// use like so:
someArray.filter(isDefined);
```

## Arrays
There are two ways to type arrays. For an array of numbers, for example:

1. Generic: `Array<number>` 
2. Shorthand: `number[]`

These are equivalent.
