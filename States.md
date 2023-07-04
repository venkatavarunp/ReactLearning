# State in React
## Component 
Components are independent and reusable bits of code.
 
They serve the same purpose as JavaScript functions, but work in isolation and return HTML.
## State 
React components has a built-in `state` object.

The `state` object is where you store property values that belong to the component.

When the `state` object changes, the component re-renders.

### Sample code
```javascript
class CartItem extends React.Component{
    constructor(){
        super();
        this.state={
            price:999,
            title:'Phone',
            qty:1,
            img:''
        }
    }
```
`CartItem` is an example of component and `state` represents the state.
# setState
we can change the change the value of a state using `setState`.

### Sample code
```javascript
increaseQuantity=()=>{
        // setState form1
        this.setState({
            qty:this.state.qty+1
        });
        // setState form2
        this.setState((prevState)=>{
            return {
                qty:prevState.qty+1
            }
        });
    }
```
### setState for event handlers
the `setState` for event handlers is asynchronous so react provides an call back function that excutes after the state changes.
### Sample Code
```javascript
increaseQuantity=()=>{
        // setState form1
        this.setState({
            qty:this.state.qty+1
        },()=>{
          console.log(this.state);
        });
        // setState form2
        this.setState((prevState)=>{
            return {
                qty:prevState.qty+1
            }
        },()=>{
          console.log(this.state);
        });
    }
```
