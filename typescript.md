# Typescript

Notes from Kent Dodds lessons
 - install typescript: `npm install --save-dev typescript`
 - create a config file, `tsconfig.json`
 - Tell typescript not to compile (Babel can do that); just identify problems:
 
 ```json
 {
  "compilerOptions": {
    "noEmit": true,
    "baseUrl": "./src"
  }
}

 

