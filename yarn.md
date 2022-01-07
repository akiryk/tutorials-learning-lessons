# Yarn

## Resources
- [All about versions and operators](https://classic.yarnpkg.com/en/docs/dependency-versions)
- [Common yarn commands](https://classic.yarnpkg.com/en/docs/usage) (`yarn` and `yarn install` do the same thing)
- [docs for CLI commands](https://classic.yarnpkg.com/en/docs/cli/)
- [manage dependencies](https://classic.yarnpkg.com/en/docs/managing-dependencies) e.g.:

### Examples
If you want to add a peer dependency with more than one optional version:
```json
"peerDependencies": {
  "grunt": "^1.3 || ^1.4",
}
```
do this:
```sh
yarn add --peer "grunt@^1.3 || ^1.4"
```
