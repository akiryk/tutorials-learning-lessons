# Nextjs

## Progress:
I'm currently up [to here](https://nextjs.org/learn/basics/assets-metadata-css)

## Styling with Typescript
See [this documentation](https://tailwindcss.com/docs/guides/nextjs) but you need to add one thing, which is a global.css file and a way to import it. 

- at the top level, add a directory called styles with a globals.css, `/styles/globals.css`
- in `/pages/` add a file called `_app.js` or `_app.ts`
- in that file, add this:

```jsx
import "../styles/globals.css";

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

export default MyApp;
```
