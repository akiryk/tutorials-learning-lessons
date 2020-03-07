# Render Props

Render props provide a way to share non-visual logic between components. They can often be replaced with custom hooks. To use render props:

## The logic-providing component

1. Make a component that takes a prop that by convention is called `render`
2. The `render` prop should be a function
3. Provide some logic that calls the function and passes it some data

### Example

```js
const Hoverable = ({render}) => {
  const [isHovering, setIsHovering] = React.useState(false);
  const handleMouseOver = () => setIsHovering(true);
  const handleMouseOut = () => setIsHovering(false);
  return (
    <div 
      onMouseOver={handleMouseOver}
      onMouseOut={handleMouseOut}
    >
      {render(isHovering)}
    </div>
  )
}
```

## The logic-consuming component

1. Render the logic-providing component
2. It's children should be a function that expects to receive an argument or arguments and does something with those arguments.

### Example 

```js
const Graphic = props => (
  <Hoverable>
    {isHovering => isHovering ? (
          <div>{props.graphic}</div>
        ) : (
          <div>{props.teaser}</div>
        )
     }
   </Hoverable>
)
```
 
 
