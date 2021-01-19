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
    "module": "commonjs",
    "target": "ES2017",
    "outDir": "lib"
  },
  "include": ["src"]
}
```
The above will create your ts files in `lib/` folder and will compile them to work with ES2017.
