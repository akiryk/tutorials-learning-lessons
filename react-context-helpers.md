# React Context Helpers

```js
import React, {useContext} from 'react';

export const MyContext = React.createContext();

export function MyContextProvider({value, children}) {
  return (
    <MyContext.Provider value={value}>
      {children}
    </MyContext.Provider>
  );
}

/* :: type ConsumerProps = {
  children: (props: MyContext) => Node,
};*/

export function useMyContext() {
  const props = useContext(MyContext);
  if (!props) {
    throw new Error(
      'MyContextConsumer must be used within a MyContextProvider'
    );
  }

  return props;
}

export function MyContextConsumer({children}) {
  const props = useMyContext();

  return children(props);
}

export function withMyContext(Component) {
  const displayName = `withMyContext(${
    Component.displayName || Component.name
  })`;

  const componentContainer = (props) => (
    <MyContextConsumer>
      {(contextProps) => (
        <Component {...props} contextProps={contextProps} />
      )}
    </MyContextConsumer>
  );
  componentContainer.displayName = displayName;

  return componentContainer;
}
```
