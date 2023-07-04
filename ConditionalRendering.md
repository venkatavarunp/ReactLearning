# Conditional Rendering
we can slowly display a rendering comments to the page while the app datat is being fetched from the server 
```javascript
function App() {
  const userName="Varun",isLoggedIn=false,loading=false;
  if (loading){
    return <h1>Loading Please Wait!</h1>
  }
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Hello {isLoggedIn?userName:"Guest"}
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```
the conditions can also be written as 
```javascript
function App() {
  const userName="Varun",isLoggedIn=false,loading=false;
  if (loading){
    return <h1>Loading Please Wait!</h1>
  }
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        {!isLoggedIn && <p>Hello Guest</p>}
        {!isLoggedIn && <p>Hello {name}/p>}
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```
