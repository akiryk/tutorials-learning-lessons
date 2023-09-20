# Node CLI

The idea of a node cli is a program you can run from anywhere on your computer with a single command. We enable this functionality with two things:

1. Add `bin` to your package.json that names your command and points to the entry point
2. Add hashbang to the top of the entry point pointing to `which node` you use
3. run `npm link`

```js
// package.json
  "license": "ISC",
  "bin": {
    "myCommand": "./index.js"
  }
}

// index.js at the very top of the file
#!/usr/bin/env node
```
