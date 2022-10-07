# RegEx

## Useful snippets

```js
// find text between delimiters
const text = 'Hello and @welcome@ back!';
const [a, b, c] = text.match('(.*)@(.*)@');
// a will be "Hello and @welcome@
// b will be "Hello and ";
// c will be "welcome";
```
