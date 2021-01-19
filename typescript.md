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

## Variables
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

## Arrays 
```js
let aa: number[] = [];
aa.push(33);
aa.push("abc"); // 🚨 ERROR: Argument of type '"abc"' is not assignable to parameter of type 'number'.

// an array of "nevers"; it will never work
let aa = [];
aa.push(33); // ERROR

// "Tupple" an array of fixed length; follows a convention
```

For lots more examples, see the [course notes for basics.ts](https://github.com/mike-works/typescript-fundamentals/blob/master/notes/1-basics.ts)

