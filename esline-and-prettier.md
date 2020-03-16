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
