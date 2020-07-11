Links: [[202007111223 JavaScript fundamentals before learning React]]

# React and JavaScript classes
#react #js

## JavaScript Classes
```javascript
class Developer {
	constructor(firstname, lastname) {
    	this.firstname = firstname;
    	this.lastname = lastname;
  	}
 
  	getName() {
    	return this.firstname + ' ' + this.lastname;
  	}
}
 
var me = new Developer('Robin', 'Wieruch');
 
console.log(me.getName());
```

- **Class** describes **entity**
- **Entity** used as blueprint to create an **instance**
- When class **instance** is going to be created by `new` statement, the **constructor** of the class is called
- **Class** have **properties**, which located in **constructor**
- **Class methods**, such as `getName()`, is used to read/write data of the **instance**
- **Class instance** represented as `this` object inside this **class**
- Outside, **instance** assigned to **variable**
- **Classes** used for **inheritance** in **OOP**
- `extends` statement can be used to inherit one class from another

```javascript
...
 
class ReactDeveloper extends Developer {
	getJob() {
    	return 'React Developer';
  	}
}
 
var me = new ReactDeveloper('Robin', 'Wieruch');

...
console.log(me.getJob());
```

- **JavaScript class** is used for **defining** a **React component**
- **React component** = "React Component", which inherits all abilities from React `Component` class

```jsx
import React, { Component } from 'react';
 
class App extends Component {
	render() {
    	return (
      		<div>
        		<h1>Welcome to React</h1>
      		</div>
    	);
  	}
}
 
export default App;
```

- `render()` method is mandatory in React class components - React Component instructs to use it for displaying something in browser
- Without extending from React Component, we cannot use **lifecycle methods**, such as `componentDidMount()` and `this.setState()`

```jsx
import React, { Component } from 'react';
 
class App extends Component {
	getGreeting() {
    	return 'Welcome to React';
  	}
 
  	render() {
    	return (
      		<div>
        		<h1>{this.getGreeting()}</h1>
      		</div>
    	);
  	}
}
 
export default App;
```

## Summary
1. JavaScript classes used for defining React components, when we need access to React API:
	- lifecycle methods
	- `this.state`
	- `this.setState()`
2. React favors composition over inheritance (see [[202007111251 React Composition vs Inheritance]])