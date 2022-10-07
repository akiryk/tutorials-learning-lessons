# HOC

The Higher Order Component pattern is a way to share non-visual logic between components. Alternatives include Render Props and Custom Hooks.

## The Higher Order Component

1. Make a function, by convention prefixed by `with`
2. This function returns a component that takes a component as a prop.
3. Handle logic in some way and pass the results as a prop to the component.

### Example

```js
export const withHover = Component => {
  return class Hover extends React.Component {
    state = {
      isHovering: false
    }
    
    handleMouseOver() {
      this.setState({isHovering: true});
    }
    
    handleMouseOut() {
      this.setState({isHovering: false});
    }
    
    render() {
      return (
        <div 
          onMouseOver={this.handleMouseOver}
          onMouseOut={this.handleMouseOut}
        >
          <Component isHovering={this.state.isHovering}>
        </div>
       )
     }
  }   
}

const SomeComponent = props => {
  return (
    {props.isHovering ? (
      <p>One Things</p>
    ) : (
      <p>Another Things</p>
    )}
  )
}

export default withHover(SomeComponent);
```
