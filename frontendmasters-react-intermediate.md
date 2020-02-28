# React Intermediate

## Hooks

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
