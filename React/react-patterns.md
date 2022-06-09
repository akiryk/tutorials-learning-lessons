# React Patterns

## useEffect Patterns

`useEffect` is really for synchronization, not all the other things it's used for. Effects go in event handlers. Render as you fetch with suspense.

### Fetch on Render

Do not use `useEffect` according to [David Khourshid](https://www.youtube.com/watch?v=HPoC-k7Rxwo)

1. useEffect way, which he doesn't suggest

```js
function Component() {
  const [data, setData] = useState(null);
  useEffect(() => {
    let canceled = false;
    fetch("some/resource").then((data) => {
      if (canceled) return;
      setData(data);
    });

    return () => {
      canceled = true;
    };
  }, []);

  return; //
}
```

2. Better to use suspense or the Remix `loader` or Next's `getServerSideProps`

```js
const data = someResource.read();

return; // ...
```

### Run only once

```js
const executedRef = useRef(false);

useEffect(
  () => {
    if (executedRef.current) {
      return;
    }
    // else
    doSomething();
    executedRef.current = true;
  },
  [
    /*...*/
  ]
);
```

## State

`useState` can default to a different value depending on a condition

```js
const [state, setState] = () => {
  return someCondition ? "oneState" : "anotherState";
};
```

## Component Patterns

### Compound Components

Compound components provide a more expressive and flexible API for communication between the parent and the child components.
[Article](https://www.smashingmagazine.com/2021/08/compound-components-react/#:~:text=The%20objective%20of%20compound%20components,parent%20and%20the%20child%20components.&text=Compound%20components%20in%20React%20are,helps%20to%20avoid%20prop%20drilling.)
