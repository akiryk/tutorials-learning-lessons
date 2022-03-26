# React Patterns

## State
`useState` can default to a different value depending on a condition
```js
const [state, setState] = () => {
  return someCondition ? 'oneState' : 'anotherState'
}
```

## Component Patterns

### Compound Components
Compound components provide a more expressive and flexible API for communication between the parent and the child components.
[Article](https://www.smashingmagazine.com/2021/08/compound-components-react/#:~:text=The%20objective%20of%20compound%20components,parent%20and%20the%20child%20components.&text=Compound%20components%20in%20React%20are,helps%20to%20avoid%20prop%20drilling.)
