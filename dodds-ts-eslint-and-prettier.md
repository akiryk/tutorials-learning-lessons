# Typescript, Eslint, and Prettier

## Prettier

- Install the VSCode Prettier extension (or extension for whatever your code editor is)
- Create a `.prettierrc` file for your own custom config options
- Go to [prettier.io/playground](https://prettier.io/playground) to customize your configs; paste into the config file
- Go to user settings and set editor configurations like so:
    - `"editor.formatOnSave": true`
    - `"editor.defaultFormatter": "esbenp.prettier-vscode"`

## Eslint

Since Prettier will clean up certain Eslint mistakes automatically, anyway, no need to be alerted. You can install eslint-config-prettier and then add it as an extension.

```sh
# terminal
npm install --save-dev eslint-config-prettier

# add to .eslint
 "extends": ["eslint:recommended", "eslint-config-prettier"],
 ```

## Typescript

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
    "validate": "npm-run-all --parallel check-types check-format lint build"
 }
 ```
   
