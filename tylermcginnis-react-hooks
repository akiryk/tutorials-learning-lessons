# React Hooks - Tyler McGinnis tutorial

From [Online Series](https://learn.tylermcginnis.com/courses/613356/lectures/10985808)

## Why Hooks?
- React has no good native solution for sharing non-visual logic
- Lifecycle methods mean we sprinkle related logic or duplicate logic throughout our code
- using `this` can be annoying/confusing

There are three main things that class components enable us to handle that function components must also handle:
1. State
2. Synchronization 
3. Sharing non-visual logic

- *State* is handled by `useState` vs `setState`
- *Synchronization* is handled by `useEffect` vs life cycle methods. Note: don't think of this as simply replacement for lifecycle methods because it's a different mental model.
- *Sharing* is handled by custom hooks

## useState

`useState` allows you to: 
- trigger a component re-render, 
- and it can preserve values between renders.

`useState` takes an argument that can be a value or a function.
- when passed a value, it gets called every time the component renders. E.g. `const [x, setX] = useState(getX())` will call getX() every time.
- when passed a function, it will invoke it only once, on the first render. E.g.  `const [x, setX] = useState(() => getX())` will call getX() only once. This is called *lazy initialization*.

`setState` takes either value or a function
- pass a value when it doesn't depend on the previous value
- pass a function when it does: `setCounter(prevCount => prevCount + 1)`

## useEffect
1. Add an effect with `useEffect()`
2. Skip re-invoking an effect by passing an array
3. Clean up the effect by having it return a function that performs cleanup logic.

*When useEffect runs* The first time that a component renders
1. React first renders the UI
2. React then runs the side effect.
*If the component re-renders (say, a prop changes)*
1. Render the UI
2. Run the cleanup function
3. Invoke the side effect

## Custom Hooks
*Why use them?* They enable us to share non-visual logic. They are an alternative to Higher Order Components, e.g. `withHover`, and Render Props. 

*What's wrong with HOCs and Render Props?*
- They don't compose well
- Logic can be hard to follow
- Force you to restructure the render tree

How to make a custom hook
1. Give it a name beginning with `use`
2. It must return a value -- could be an object, a string, a boolean.
3. It can use `useState` or any other hooks

## useReducer
- more declarative than `useState`
- because the reducer function is passed the current state, it's easier to update state of app based on the previous state
- enables us to minimize the dependency array of `useEffect`. How? Compare:
```js
// In first case, we need to pass count as a dependency, but this means we start a new interval every time count changes
useEffect(() => {
  const id = window.setInterval(() => {
    setCount(count + 1);
  }, 1000);
  
  return function() {
    clearInterval(id);
  }
}, [count]); 

// In second case, we don't have any dependencies
useEffect(() => {
  const id = window.setInterval(() => {
    dispatch({type: 'increment');
  }, 1000);
  
  return function() {
    clearInterval(id);
  }
}, []); 

// Note that if all you wanted was an incrementer, you could alternatively remove dependencies by passing setState a function:
useEffect(() => {
  const id = window.setInterval(() => {
    setCount(prevCount => prevCount + 1)
  }, 1000);
  
  return function() {
    clearInterval(id);
  }
}, []); 
```

### When to choose useState vs useReducer
Use `useState` when:
- the values in your state tend to be updated independently

Use `useReducer` when:
- the values in your state tend to be updated together or
- updating one piece of state depends on another

### How to use useReducer
```js
// it gives us a reference to state and to the dispatch function
// we pass it a reducer funtion and initial state
const [state, dispatch] = useReducer(reducerFn, initialState);
```

## useRef
Both `useRef` and `useState` enable you to persist state across renders. In contrast to `useState`, `useRef` does *not* trigger a rerender, however. Use it when you want to:
- persist state
- not trigger a rerender

## useContext

- create context in the same way
- use a context provider as before
- instead a function providing the context value to consumers, the consumers use `useContext`

```js
// my_context.js
import React from 'react';

const MyContext = React.createContext();

export default MyContext;

// end my_context.js ------------------------

// app.js
import React from 'react';
import MyContext from 'my_context';
import VariousComponents from 'various_components';

const App = () => {
  return (
    <MyContext.Provider value={someValue}>
      <VariousComponents />
    </MyContext.Provider>
  )
}

// end app.js ------------------------

// some consumer
import React from 'react';
import MyContext from 'my_context';

const SomeConsumer = () => {
  const someValue = React.useContext(MyContext);
  return (
    <h1>I got {someValue}</h1>
  )
}
```
