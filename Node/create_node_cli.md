# Node CLI

The idea of a node cli is a program you can run from anywhere on your computer with a single command. We enable this functionality with two things:

1. Add `bin` to your package.json that names your command and points to the entry point
2. Add hashbang to the top of the entry point telling which execution environment to use. This path will be the same across all platforms, and you can use it for any environment: `usr/bin/env python`, etc. What you're doing here is running a program, the `env` program, which is locaed in `usr/bin`. 
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
