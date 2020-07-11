Links: [[202007111228 React and JavaScript classes]]

# React Composition vs Inheritance
#react #article #inheritance
> React has a powerful composition model, and we recommend using composition instead of inheritance to reuse code between components. -- [reactjs.org](https://reactjs.org/docs/composition-vs-inheritance.html)

## Containment

### Problem
- Some components don't know their children
- Situation is common for components like `Sidebar`, `Dialog` etc., that represents generic "boxes"

### Solution
- Use special `children` prop to pass children elements directly into their output

### Examples

```jsx
function FancyBorder(props) {
	return (
		<div className={'FancyBorder FancyBorder-' + props.color}>
			{props.children}
		</div>
	);
}
```

Now we can pass other components as children to them by nesting the JSX:

```jsx
function WelcomeDialog() {
	return (
		<FancyBorder color="blue">
      		<h1 className="Dialog-title">
	  			Welcome
			</h1>
			<p className="Dialog-message">
				Thank you for visiting our spacecraft!
			</p>
		</FancyBorder>
	);
}
```

- Anything inside `<FancyBorder>` JSX tag passed into component as `children` prop
- `FancyBorder` renders `{props.children}` inside `<div>` tag = passed elements appear in the output

Using multiple "holes"/places in a component:

```jsx
function SplitPane(props) {
	return (
		<div className="SplitPane">
			<div className="SplitPane-left">
				{props.left}
			</div>
			<div className="SplitPane-right">
				{props.right}
			</div>
		</div>
	);
}

function App() {
	return (
		<SplitPane left={<Contacts />} right={<Chat />} />
	);
}
```

- We can pass React elements to props

## Specialization
- Some components could be a "special cases" of other components, for example - `WelcomeDialog` is special case of `Dialog`

```jsx
function Dialog(props) {
	return (
		<FancyBorder color="blue">
			<h1 className="Dialog-title">
				{props.title}
			</h1>
      		<p className="Dialog-message">
        		{props.message}
			</p>
    	</FancyBorder>
	);
}

function WelcomeDialog() {
	return (
    	<Dialog
			title="Welcome"
			message="Thank you for visiting our spacecraft!" /> 
	);
}
```

Composition works also for class-based components:

```jsx
function Dialog(props) {
	return (
    	<FancyBorder color="blue">
      		<h1 className="Dialog-title">
        		{props.title}
      		</h1>
      		<p className="Dialog-message">
        		{props.message}
      		</p>
      		{props.children}
		</FancyBorder>
  	);
}

class SignUpDialog extends React.Component {
	constructor(props) {
    	super(props);
    	this.handleChange = this.handleChange.bind(this);
    	this.handleSignUp = this.handleSignUp.bind(this);
    	this.state = {login: ''};
  	}

  	render() {
    	return (
      		<Dialog title="Mars Exploration Program"
              		message="How should we refer to you?">
        		<input value={this.state.login} onChange={this.handleChange} />
				<button onClick={this.handleSignUp}>
					Sign Me Up!
				</button>
			</Dialog>
    	);
  	}

  	handleChange(e) {
  		this.setState({login: e.target.value});
  	}

  	handleSignUp() {
		alert(`Welcome aboard, ${this.state.login}!`);
  	}
}
```