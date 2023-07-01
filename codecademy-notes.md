## Presentational and Container Components

```JSX
class CounterContainer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.increment = this.increment.bind(this);
  }
  
  increment() {
    this.setState((oldState) => {
      return { count: oldState.count + 1};
    });
  }
  
  render() {
    return <Counter count={this.state.count} increment={this.increment} />;
  }
}

class Counter extends React.Component {
  render() {
    return (
    	<div>
      	<p>The count is {this.props.count}.</p>
        <button onClick={this.props.increment}>Add 1</button>
      </div>
    )
  }
}
```

A common programming pattern in React is to have presentational and container components. Container componentes contain bussiness logic and handle methods. Presentational components render that behaviour and state. `CounterContainer` is a container component and `Counter` is presentational.



## React Programming Pattern

```JSX  
// This is stateless child component
function BabyYoda(props) {
  return <h2>I am a {props.name}!</h2>
}

// This is a stateful Parent Component
function Yoda(){
  const [name, setName] = useState("Toyoda")
  
	// The child component will render the information passed down from the parent component.
	return <BabyYoda name={name} />;
}
```



## Event Handlers and State in React

```JSX
function MyComponent() {
  const [text, setText] = useState("");
  
  const HandleChange(event) => {
    setText(event.target.value);
  }
  
  return {
    <div>
    	<input onChange={HandleChange} value={text} />
      <p>You typed {text}</p>
    </div>
  }
}
```



## Changing Props and State

```JSX
function Clock(props) {
  const [ date, setDate ] = useState(new Date());
  
  const updateTime = () => {
    setDate(new Date());
  }
  
  return (
  	<div>
    	<h1>It is currently {date.toLocaleTimeString()}</h1>
      <h2>{props.subtitle}</h2>
      <button onClick={updateTime}>Update the clock</button>
    </div>
  )
}
```

A component that accepts a prop, `subtitle`, which never changes. It has a state object which does change.



## Passing State Change Function as Props

If a React parent component definies a function that changes its state, that functiona can be passed to a child component.

# React Programming Patterns

It is convenient to split complex components into stateful (container) and stateless (presentational) components. Stateful componentes manage complex state or login and stateless components only render JSX. 



## Create Container Component 

This is the functional and stateful part. It will be in charge of mantaining the state. 

The container component must define and provide a way for the presentational componente to communicate with it using a change handler function passed as a prop.



```JSX
function Container() {
  const [isActive, setIsActive] = useState(false);


return (
	<>
  	<Presentational active={isActive} toogle={setIsActive}/>
  	<OtherPresentational active={isActive} />
  </>
	);
}

function Presentational(props){
  return (
  	<h1>Engines are {props.active}</h1>
    <button onClick={() => props.toogle(!props.active)}>Engine Toogle</button>
  )
}

function OtherPresentational(props) {
  // render
}
```

