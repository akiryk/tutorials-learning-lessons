# React Intermediate

## Hooks

### useContext such that children can change the context

If you use `useState` to set the context value, then consumers can `setState` and change the value for all other consumers

```js
const PersonContext = createContext();

// the provider saves useState/setState to a single variable
const person = React.useState({name: "Bobby"});
return (
  <PersonContext.Provider value={person}>
    // etc
 
// a consumer 
// get a reference to the initial person object and to the setter method
const [person, setPerson] = React.useContext(PersonContext)
const handleClick = () => {
  // change the person's name on click
  setPerson({
    ...person,
    name: "New Name"
  });
```

### useMemo, memo, and useCallback

`React.useMemo` and `React.memo` are two different things. 
- `memo` is a HOC that takes a functional component. As long as none of its properties have changed, do not re-render. Obviously, it works best when props are value props and not, say, objects. 
- `useMemo` is a function that takes a function and returns the memoized return value of that function.
- `useCallback` is like `useMemo` but it takes both a function and an array of dependencies that tell it when to re-run.

### useLayoutEffect

Useful for measuring things on the screen. It gets called a few times in order to determine clientWidth in below example, but it only paints once.
```js
const LayoutEffectComponent = () => {
  const [width, setWidth] = useState(0);
  const [height, setHeight] = useState(0);
  const el = useRef();

  useLayoutEffect(() => {
    setWidth(el.current.clientWidth);
    setHeight(el.current.clientHeight);
  });

  return (
    <div>
      <h1>useLayoutEffect Example</h1>
      <h2>textarea width: {width}px</h2>
      <h2>textarea height: {height}px</h2>
      <textarea
        onClick={() => {
          setWidth(0);
        }}
        ref={el}
      />
    </div>
  );
};
```

## Code Splitting

`React.lazy()` enables you to load a component only at the moment you need it — i.e. when it is first rendered. 
`Suspense` is used as a wrapper around anything that contains lazy loaded components. 

**Only use lazy() if you have a module larger than approx 30kb** -according to Brian Holt, otherwise it's more effort than what you will gain. His reason is that it can be a worse UX to wait for something that loads quickly anyway. If waiting for an 800k library to load, fine, show a loader. Otherwise...

## SSR

Why?
- So that users have something to look at when page first loads as js is still downloading and being parsed

How to?
- Call `hydrate()` from react-dom not `render()`. This ensures that the content inside of `<div id="root">` isn't blown away, allowing users to see the SSR content
- Remove any uses of `document` or `window` from code that will be called server-side, since node doesn't understand them.
- In server side code, render the parts that you want to render (e.g. with express' `app.use()`)

`renderToString` compared to `renderToNodeStream`. First renders the entire thing all at once, the second breaks it into chunks, which is much better approach for large apps. See [react-dom docs](https://reactjs.org/docs/react-dom-server.html).
