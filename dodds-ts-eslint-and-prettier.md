# Typescript, Eslint, and Prettier

## tldr
```js
// in vscode settings.json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": ["javascript"],
}

// in .eslintrc
{
  "parser": "babel-eslint",
  "extends": ["eslint:recommended", "prettier"],
  "plugins": ["prettier"],
  "env": {
    "browser": true,
    "node": true
  },
  "rules": {
    "prettier/prettier": ["error"]
  }
}

// in .prettierrc
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 70,
}


```

## Prettier

- Install the VSCode Prettier extension (or extension for whatever your code editor is)
- Create a `.prettierrc` file for your own custom config options
- Go to [prettier.io/playground](https://prettier.io/playground) to customize your configs; paste into the config file
- Go to user settings and set editor configurations like so:
    - `"editor.formatOnSave": true`
    - `"editor.defaultFormatter": "esbenp.prettier-vscode"`
    
 ```sh
 npm install --save-dev prettier
 ```
 ```json
 // package.json
 scripts": {
    // we can tell prettier to "write", which saves changes matching js and json files
    // add --ignore-path so prettier knows what file to use for ignoring 
    "format": "prettier --ignore-path .gitignore --write \"**/*.+(js|json|html|css)\"",
 // etc
 ```
 
 An example `.prettierrc` config file in json format:
 ```json
 {
    "trailingComma": "es5",
    "tabWidth": 2,
    "semi": false,
    "singleQuote": true
}
 ```
 
## Eslint

Since Prettier will clean up certain Eslint mistakes automatically, anyway, no need to be alerted. You can install eslint-config-prettier and then add it as an extension.

```sh
# terminal
npm install --save-dev eslint
# add prettier config so that we don't get warnings for stuff prettier will fix
npm install --save-dev eslint-config-prettier

# add to .eslint extends both recommended and the prettier config
 "extends": ["eslint:recommended", "eslint-config-prettier"],
 ```

## Typescript

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

- To disable eslint rules, you can use `// eslint-disable-next-line <name-of-rule>`
- To disable an eslint rule for the entire file, e.g.: `/* eslint-disable strict */`

- Install preset-typescript for babel, so it can handle .ts files, `npm install --save-dev @babel/preset-typescript`;

## Husky

Install husky and create a `.huskyrc` file to enable pre-git-commit validation

## Example package.json scripts from dodds

- `--ignore-path` flag says to use a particular file for a list of what to ignore.
- Use `npm-run-all` module and command in your `validate` script to run all validations in parallel. Much faster. 


```json
"scripts {
    "build": "babel src --extensions .js,.ts,.tsx --out-dir dist",
    "lint": "eslint --ignore-path .gitignore --ext .js,.ts,.tsx",
    "prettier": "prettier --ignore-path .gitignore \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "check-types": "tsc",
    "check-format": "npm run prettier -- --list-different",
    // validate simply assures that project is in a good state; run-all in parallel is faster than not in parallel
    "validate": "npm-run-all --parallel check-types check-format lint build"
 }
 ```
   
