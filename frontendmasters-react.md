# Front End Masters, 
Notes from [Front End Masters](https://frontendmasters.com/courses/complete-react-v5/) course

- Error Boundaries
- Modals
 
## Error Boundary

*Error Boundary must be a class component*

```js
// No!
const ErrorBoundary = props => {
  const [errors, setErrors] = React.useState(false);
  // etc.
 
// Yes!
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  // etc.
```

*Error Boundary only catch errors in components below them in the tree*

```js
// No! Error Boundary won't catch errors inside MyComponent (although it will catch anything thrown in Carousel)
class MyComponent {
  componentDidMount() {
    // Say this throws an error while getting some data...
  }

  render() {
    return (
      <MyErrorBoundaryComponent>
        <h1>Title</h1>
        <Carousel data={props.data} />
      </MyErrorBoundaryComponent>
    )
  }
 
// Yes! This will catch errors in both MyComponent and in Carousel.
class MyComponent {
  componentDidMount() {
    // Say this throws an error while getting some data...
  }
  render() {
     // etc
   }
}

const MyComponentWithErrorBoundary = props => (
    <ErrorBoundary>
      <MyComponent {...props}>
    </ErrorBoundary>
  )

export default MyComponentWithErrorBoundary
```

*Show UI with getDerivedStateFromError*

```js
state = { hasError: false };

static getDerivedStateFromError() {
  return { hasError: true };
}
```

### Log errors with componentDidCatch

```js
componentDidCatch(error, errorInfo) {
  // You can also log the error to an error reporting service
  logErrorToMyService(error, errorInfo);
}
```

## Modals

React uses something called `portals`

- In addition to your `<div id="root">` element, you should have one called `<div id="modal">`
- Create a `Modal` component that imports `createPortal` from 'react-dom'
- use `useRef()` to create a reference to the "modal" div element

```js
import React, { useEffect, useRef } from "react";
import { createPortal } from "react-dom";

const Modal = ({ children }) => {
  const elRef = useRef(null);

  if (!elRef.current) {
    elRef.current = document.createElement("div");
  }

  useEffect(() => {
    const modalRoot = document.getElementById("modal");
    modalRoot.appendChild(elRef.current);

    return () => modalRoot.removeChild(elRef.current);
  });

  return createPortal(<div>{children}</div>, elRef.current);
};
