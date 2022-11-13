# Subscriber Pattern

## The Store
First, you need a store. Create with a function or a class:

```js
export const createStore = (initialState) => {
  let currentState = initialState;
  let listeners = new Set();
  return {
    getState: () => currentState,
    setState: (newState) => {
      currentState = newState;
      listeners.forEach((listener) => listener(currentState));
    },
    subscribe: (fn) => {
      listeners.add(fn);
      return () => listeners.delete(fn);
    }
  };
};

// Class
class Store {
  constructor(initialState) {
    this.state = initialState;
    this.listeners = new Set();
  }

  getState() {
    return this.state;
  }

  setState(state) {
    this.state = state;
    this.listeners.forEach((listener) => listener(this.state));
  }

  subscribe(subscriberFunction) {
    this.listeners.add(subscriberFunction);
    return () => this.listeners.delete(subscriberFunction);
  }
}
```

## Use the store
Use the store by creating or instantiating the store and passing in some initial state:
```js
const store = createStore(initialState);
```

Then get the store or set the store like so
```js
const onClick = () => {
  const state = store.getState();
  store.setState({
    ...state,
    [item]: state[item] + 1
  });
};
```

Avoid unnecessary rerenders by using selectors. 
```js
const useSubscribeToStore = (selector) => {
  const [state, setState] = useState(selector(store.getState));
  
  useEffect(() => {
    store.subscribe((state) => {
      setState(selector(state));
    });
  }, [selector]);
  
  return state;
}
```

Now you can use the store in components that need it
```
const SomeConsumer = ({id}) => {
    const selector = state => state[id];
    const state = useSubscribeToStore(selector);
}
