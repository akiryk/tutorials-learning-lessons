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
```

- Install preset-typescript for babel, so it can handle .ts files, `npm install --save-dev @babel/preset-typescript`;
- Use `npm-run-all` module and command in your `validate` script to run all validations in parallel. Much faster. 

### Example package.json scripts from dodds

- `--ignore-path` flag says to use a particular file for a list of what to ignore.

```json
"scripts {
    "build": "babel src --extensions .js,.ts,.tsx --out-dir dist",
    "lint": "eslint --ignore-path .gitignore --ext .js,.ts,.tsx",
    "prettier": "prettier --ignore-path .gitignore \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "check-types": "tsc",
    "check-format": "npm run prettier -- --list-different",
    "validate": "npm-run-all --parallel check-types check-format lint build"
 }
 ```
   
