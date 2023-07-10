# Component
seperate blocks of html,css,js that is independent and can be reusable.
## Passing Data via Props
components can't pass the data for themselves we can use props to pass the data from component to another component
```javascript
import ExpenseItem from "./components/ExpenseItem";
function App() {
  const expenses = [
    {
      id: 'e1',
      title: 'Toilet Paper',
      amount: 94.12,
      date: new Date(2020, 7, 14),
    },
    { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
    {
      id: 'e3',
      title: 'Car Insurance',
      amount: 294.67,
      date: new Date(2021, 2, 28),
    },
    {
      id: 'e4',
      title: 'New Desk (Wooden)',
      amount: 450,
      date: new Date(2021, 5, 12),
    },
  ];
  return (
    <div>
      <ExpenseItem title={expenses[0].title} amount={expenses[0].amount} date={expenses[0].date}/>
      <ExpenseItem title={expenses[1].title} amount={expenses[1].amount} date={expenses[1].date}/>
      <ExpenseItem title={expenses[2].title} amount={expenses[2].amount} date={expenses[2].date}/>
      <ExpenseItem title={expenses[3].title} amount={expenses[3].amount} date={expenses[3].date}/>
    </div>
  );
}

export default App;
```
```javascript
import "./ExpenseItem.css"
function ExpenseItem(props){
  return (
    <div className="expense-item">
      <div>{props.date.toString()}</div>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
    </div>
  )
}

export default ExpenseItem;
```
can also be written as 
```javascript
import ExpenseItem from "./components/ExpenseItem";
function App() {
  const expenses = [
    {
      id: 'e1',
      title: 'Toilet Paper',
      amount: 94.12,
      date: new Date(2020, 7, 14),
    },
    { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
    {
      id: 'e3',
      title: 'Car Insurance',
      amount: 294.67,
      date: new Date(2021, 2, 28),
    },
    {
      id: 'e4',
      title: 'New Desk (Wooden)',
      amount: 450,
      date: new Date(2021, 5, 12),
    },
  ];
  return (
    <div>
      <ExpenseItem expense={expenses[0]}/>
      <ExpenseItem expense={expenses[1]}/>
      <ExpenseItem expense={expenses[2]}/>
      <ExpenseItem expense={expenses[3]}/>
    </div>
  );
}

export default App;
```
```javascript
import "./ExpenseItem.css"
function ExpenseItem(props){
  return (
    <div className="expense-item">
      <div>{props.expense.date.toString()}</div>
      <div className="expense-item__description">
        <h2>{props.expense.title}</h2>
        <div className="expense-item__price">${props.expense.amount}</div>
      </div>
    </div>
  )
}

export default ExpenseItem;
```
we can also use object destructuring on the receiving end
```javascript
import "./ExpenseItem.css"
function ExpenseItem({date,title,amount}){
  return (
    <div className="expense-item">
      <div>{date.toString()}</div>
      <div className="expense-item__description">
        <h2>{title}</h2>
        <div className="expense-item__price">${amount}</div>
      </div>
    </div>
  )
}

export default ExpenseItem;
```
# Composition
To eliminate code duplication 

we can't use wrapper component around the components by default
```javascript
import ExpenseItem from "./ExpenseItem"
import Card from "./Card"
import "./Expenses.css"
const Expenses = (props) => {
  return (
      <Card className="expenses">
        <ExpenseItem title={props.items[0].title} amount={props.items[0].amount} date={props.items[0].date}/>
        <ExpenseItem title={props.items[1].title} amount={props.items[1].amount} date={props.items[1].date}/>
        <ExpenseItem title={props.items[2].title} amount={props.items[2].amount} date={props.items[2].date}/>
        <ExpenseItem title={props.items[3].title} amount={props.items[3].amount} date={props.items[3].date}/>
      </Card>
  )
}

export default Expenses;
```
we can place the repeated code in the wrapper component 
```javascript
import './Card.css';
const Card = (props) => {
  // sets the properties for all the classes
  const classes='card '+props.className;
  return <div className={classes}>{props.children}</div>;
}

export default Card;
```
