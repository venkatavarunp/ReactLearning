
# State and Events
## Event Handlers
Event Handlers can be used to listen for the events that occurs on the HTML components

These basically start with `on`
## State 
to update the values of any of the components we use `state` specifcallu `useState` function which return the value to be changed and the function to change the state.
```javascript
import ExpenseDate from "./ExpenseDate";
import Card from "./Card";
import "./ExpenseItem.css";
import { useState } from "react";
const ExpenseItem = (props) => {
  const [title, setTitle] = useState(props.title);

  const clickHandler = () => {
    setTitle("Updated");
  };
  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        <h2>{title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
};

export default ExpenseItem;
```
## Multiple States 
we can handle multiple states using previous state function but it is not preferable and we can have individual states 
```javascript
const ExpenseForm = () => {
  const [userInput, setUserInput] = useState({
    eneteredTitle: "",
    eneteredAmount: "",
    eneteredDate: ""
  });

  const titleHandler = (event) => {
    setUserInput( (prevState) => {
      return{...prevState, eneteredTitle:event.target.value}
    });
  }
  const amountHandler = (event) => {
    setUserInput( (prevState) => {
      return{...prevState, eneteredTitle:event.target.value}
    });
  };
  const dateHandler = (event) => {
    setUserInput( (prevState) => {
      return{...prevState, eneteredTitle:event.target.value}
    });
  };
```
we can write all the handler functions in a single function as below
```javascript
import { useState } from "react";
import "./ExpenseForm.css";
const ExpenseForm = () => {
  const [enteredTitle, setEnteredTitle] = useState("");
  const [enteredAmount, setEnteredAmount] = useState("");
  const [enteredDate, setEnteredDate] = useState("");

  const inputHandler = (identifier, value) => {
    if ((identifier = "title")) {
      setEnteredTitle(value);
    } else if ((identifier = "date")) {
      setEnteredDate(value);
    } else {
      setEnteredAmount(value);
    }
  };

  return (
    <form>
      <div className="new-expense__controls">
        <div className="new-expense__control">
          <label>Title</label>
          <input
            type="text"
            onChange={(event) => inputHandler("title", event.target.value)}
          />
        </div>
        <div className="new-expense__control">
          <label>Amount</label>
          <input
            type="number"
            onChange={(event) => inputHandler("title", event.target.value)}
          />
        </div>
        <div className="new-expense__control">
          <label>Date</label>
          <input
            type="date"
            onChange={(event) => inputHandler("title", event.target.value)}
            min="2019-01-01"
            max="2023-12-31"
          />
        </div>
      </div>
      <div className="new-expense__actions">
        <button type="submit">Add Expense</button>
      </div>
    </form>
  );
};

export default ExpenseForm;
```
## Two Way Binding
we can pass the inputs to elements

By this way we can store the data submitted in the form and reset it after it is submitted
```javascript
import { useState } from "react";
import "./ExpenseForm.css";
const ExpenseForm = () => {
  const [enteredTitle, setEnteredTitle] = useState("");
  const [enteredAmount, setEnteredAmount] = useState("");
  const [enteredDate, setEnteredDate] = useState("");

  const titleHandler = (event) => {
    setEnteredTitle(event.target.value);
  };
  const amountHandler = (event) => {
    setEnteredAmount(event.target.value);
  };
  const dateHandler = (event) => {
    setEnteredDate(event.target.value);
  };
  const submitHandler = (event) => {
    event.preventDefault();
    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate)
    };
    // making the state of elements as null after form is submitted
    setEnteredTitle("");
    setEnteredAmount("");
    setEnteredDate("");
  };
  return (
    <form onSubmit={submitHandler}>
      <div className="new-expense__controls">
        <div className="new-expense__control">
          <label>Title</label>
          <input type="text" value={enteredTitle} onChange={titleHandler} />
        </div>
        <div className="new-expense__control">
          <label>Amount</label>
          <input type="number" value={enteredAmount} onChange={amountHandler} />
        </div>
        <div className="new-expense__control">
          <label>Date</label>
          <input
            type="date"
            onChange={dateHandler}
            min="2019-01-01"
            max="2023-12-31"
            value={enteredDate}
          />
        </div>
      </div>
      <div className="new-expense__actions">
        <button type="submit">Add Expense</button>
      </div>
    </form>
  );
};

export default ExpenseForm;
```
## Child to Parent Component Communication
In order to pass the values from child to parent component we need to add props to the parent component (function) and pass the values using props.

**Parent Component**
```javascript
import "./NewExpense.css";
import ExpenseForm from "./ExpenseForm";
const NewExpense = () => {
  const SaveExpenseDataHandler = (enteredExpenseData) => {
    const expenseData = {
      ...enteredExpenseData,
      id: Math.random().toString()
    };
    console.log(expenseData);
  };
  return (
    <div className="new-expense">
      <ExpenseForm onSaveExpenseData={SaveExpenseDataHandler} />
    </div>
  );
};

export default NewExpense;
```
**Child Comnponent**
```javascript
const submitHandler = (event) => {
    event.preventDefault();
    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate)
    };
    props.onSaveExpenseData(expenseData);
    setEnteredTitle("");
    setEnteredAmount("");
    setEnteredDate("");
  };
``` 
