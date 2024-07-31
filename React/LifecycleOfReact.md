# React Component Lifecycle Methods – Explained with Examples

In React, components have a lifecycle that consists of different phases. Each phase has a set of lifecycle methods that are called at specific points in the component's lifecycle. These methods allow you to control the component's behavior and perform specific actions at different stages of its lifecycle.

A component's lifecycle has three main phases: the Mounting Phase, the Updating Phase, and the Unmounting Phase.

The Mounting Phase begins when a component is first created and inserted into the DOM. The Updating Phase occurs when a component's state or props change. And the Unmounting Phase occurs when a component is removed from the DOM.

## Component Mounting Phase

The mounting phase refers to the period when a component is being created and inserted into the DOM.

During this phase, several lifecycle methods are invoked by React to enable the developer to configure the component, set up any necessary state or event listeners, and perform other initialization tasks.

The mounting phase has three main lifecycle methods that are called in order:

### The `constructor()` lifecycle method

The `constructor()` method is called when the component is first created. You use it to initialize the component's state and bind methods to the component's instance. Here's an example:

```jsx
import React, { Component } from "react";

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState((prevState) => ({
      count: prevState.count + 1,
    }));
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

In this example, the `constructor()` method sets the initial state of the component to an object with a `count` property set to `0`, and binds the `handleClick` method to the component's instance. The `handleClick` method increments the `count` state property when the button is clicked.

### The `render()` lifecycle method

The `render()` method is responsible for generating the component's virtual DOM representation based on its current props and state. It is called every time the component needs to be re-rendered, either because its props or state have changed, or because a parent component has been re-rendered.

In the above example in the constructor part:

```jsx
render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

The `render` method displays the current count value and a button. When the button is clicked, the `handleClick` method is invoked. This triggers a state update, causing a re-render, and the updated count is displayed.

### The `getDerivedStateFromProps()` lifecycle method

`getDerivedStateFromProps()` is a lifecycle method available in React 16.3 and later versions that is invoked during the mounting and updating phase of a component.

During the mounting phase, `getDerivedStateFromProps()` is called after the constructor and before `render()`. This method is called for every render cycle and provides an opportunity to update the component's state based on changes in props before the initial render.

The signature of `getDerivedStateFromProps()` is as follows:

```
static getDerivedStateFromProps(props, state)
```

It takes two parameters:

`props`: The updated props for the component.

`state`: The current state of the component.

The method should return an object that represents the updated state of the component, or `null` if no state update is necessary.

It's important to note that `getDerivedStateFromProps()` is a static method, which means it does not have access to the `this` keyword and cannot interact with the component's instance methods or properties.

```jsx
import React from "react";
import ReactDOM from "react-dom";
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = { favoritefood: "rice" };
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({ favoritefood: "pizza" });
    }, 1000);
  }
  static getDerivedStateFromProps(props, state) {
    return { favoritefood: props.favfod };
  }
  render() {
    return <h1>My Favorite Food is {this.state.favoritefood}</h1>;
  }
}
ReactDOM.render(<Header />, document.getElementById("root"));
```

This is a React component named Header that renders an `<h1>` element with a string that includes the value of `this.state.favoritefood`.

The component has a constructor that sets the initial state of `favoritefood` to "rice".

The `componentDidMount()` method is also defined, which is called when the component is mounted in the DOM. In this method, there's a `setTimeout()` function that updates the state of `favoritefood` to "pizza" after 1 second (1000 milliseconds).

The component also has a static `getDerivedStateFromProps()` method that takes `props` and `state` as arguments and returns an object with a key of `favoritefood` and a value of `props.favfod`. This method is called during the mounting and updating phase of the component and is used to derive the state from props.

Finally, the component's `render()` method returns the `<h1>` element with the value of `this.state.favoritefood`.When the component is rendered using `ReactDOM.render()`, it's mounted to the element with an ID of "root".

### The `componentDidMount()` lifecycle method

The `componentDidMount()` method is called once the component has been mounted into the DOM. It is typically used to set up any necessary event listeners or timers, perform any necessary API calls or data fetching, and perform other initialization tasks that require access to the browser's DOM API.

Here's an example:

```jsx
import React from "react";
import ReactDOM from "react-dom";
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = { favoritefood: "rice" };
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({ favoritefood: "pizza" });
    }, 1000);
  }
  render() {
    return <h1>My Favorite Food is {this.state.favoritefood}</h1>;
  }
}

ReactDOM.render(<Header />, document.getElementById("root"));
```

This code defines a React component called `Header` that extends the `React.Component` class. The component has a constructor that initializes the component state with a property called `favoritefood` set to the string "rice".

The component also has a `componentDidMount` lifecycle method, which is called by React after the component has been mounted (that is, inserted into the DOM). In this method, a `setTimeout` function is used to delay the execution of a function that updates the `favoritefood` state property to "pizza" by 1 second.

Finally, the component has a `render` method that returns a JSX expression containing an `h1` element with the text "My Favorite Food is" and the current value of the `favoritefood` state property.

## Component Updating Phase

This phase occurs when a component's props or state changes, and the component needs to be updated in the DOM.

### The `shouldComponentUpdate()` lifecycle method

The `shouldComponentUpdate()`  method is called before a component is updated. It takes two arguments: `nextProps` and `nextState`. This method returns a boolean value that determines whether the component should update or not. If this method returns true, the component will update, and if it returns false, the component will not update.

Here's an example of how to use `shouldComponentUpdate()`:

```jsx
import React, { Component } from "react";
import ReactDOM from "react-dom";

class Header extends Component {
  constructor(props) {
    super(props);
    this.state = { favoriteFood: "rice" };
  }

  shouldComponentUpdate(nextProps, nextState) {
    // Only re-render if the favoriteFood state has changed
    return this.state.favoriteFood !== nextState.favoriteFood;
  }

  changeFood = () => {
    this.setState({ favoriteFood: "Pizza" });
  };

  render() {
    return (
      <div>
        <h1>My Favorite Food is {this.state.favoriteFood}</h1>
        <button type="button" onClick={this.changeFood}>
          Change food
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Header />, document.getElementById("root"));
```

The above code defines a `Header` component that displays the user's favorite food and allows the user to change it by clicking a button. The `shouldComponentUpdate()` method is implemented to only re-render the component if the `favoriteFood` state has changed, which is a good way to optimize performance.

The code uses ES6 syntax to define the component class and its methods, and imports `Component` from `React` to create the class. The `ReactDOM.render()` function is used to render the Header component to the DOM.

### The `componentWillUpdate()` lifecycle method

`componentWillUpdate()` is a lifecycle method in React that gets called just before a component's update cycle starts. It receives the next prop and state as arguments and allows you to perform any necessary actions before the component updates.

But this method is not recommended for updating the state, as it can cause an infinite loop of rendering. It is primarily used for tasks such as making API calls, updating the DOM, or preparing the component to receive new data. `componentWillUpdate()` is often used in conjunction with `componentDidUpdate()` to handle component updates.

```jsx
import React, { Component } from "react";
import ReactDOM from "react-dom";

class MyComponent extends Component {
  state = {
    count: 0,
  };

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  };

  componentWillUpdate(nextProps, nextState) {
    if (nextState.count !== this.state.count) {
      console.log(
        `Count is about to update from ${this.state.count} to ${nextState.count}.`
      );
    }
  }

  render() {
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button type="button" onClick={this.handleClick}>
          Increment
        </button>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<MyComponent />, rootElement);
```

In this example, the `componentWillUpdate` method is called whenever the component is about to update. In this method, we can access the `nextProps` and `nextState` arguments to check if there are any changes to the component's state or props. If there are changes, we can perform some actions or log messages before the update happens.

### The `componentDidUpdate` lifecycle method

The `componentDidUpdate()` method is a lifecycle method in React that is called after a component has been updated and re-rendered. It is useful for performing side effects or additional operations when the component's props or state have changed.

Here's an example of how to use the `componentDidUpdate()` method:

```jsx
import React, { Component } from "react";

class ExampleComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  componentDidUpdate(prevProps, prevState) {
    if (prevState.count !== this.state.count) {
      console.log("Count has been updated:", this.state.count);
    }
  }

  handleClick() {
    this.setState((prevState) => ({
      count: prevState.count + 1,
    }));
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.handleClick()}>Increment</button>
      </div>
    );
  }
}

export default ExampleComponent;
```

In this example, the `componentDidUpdate()` method is used to log a message to the console whenever the `count` state has been updated. It compares the previous state (`prevState.count`) with the current state (`this.state.count`) to check if there was a change.

Whenever the `handleClick()` method is called, the `count` state is incremented, triggering a re-render of the component. After the re-render, `componentDidUpdate()` is called, and it logs the updated count value to the console.

It's important to include a conditional check inside `componentDidUpdate()` to prevent infinite loops. If you want to update the state based on a prop change, make sure to compare the previous prop (`prevProps`) with the current prop (`this.props`) before updating the state.

Remember that `componentDidUpdate()` is not called during the initial render of the component, only on subsequent updates.

> As of React 16.3, the `componentDidUpdate()` method can receive two additional arguments: `prevProps` and `prevState`. These arguments provide access to the previous props and state values, which can be useful for performing comparisons.
>
> But if you are using a more recent version of React, you can utilize the `useEffect()` hook with dependency array to achieve similar functionality.

### The `getSnapshotBeforeUpdate` lifecycle method

The `getSnapshotBeforeUpdate()` method is called just before the component's UI is updated. It allows the component to capture some information about the current state of the UI, such as the scroll position before it changes. This method returns a value that is passed as the third parameter to the `componentDidUpdate()` method.

Here's an example of how to use `getSnapshotBeforeUpdate()` to capture the scroll position of a component before it updates:

```jsx
import React from "react";
import ReactDOM from "react-dom";

class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = { favoritefood: "rice" };
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({ favoritefood: "pizza" });
    }, 1000);
  }
  getSnapshotBeforeUpdate(prevProps, prevState) {
    document.getElementById("div1").innerHTML =
      "Before the update, the favorite was " + prevState.favoritefood;
  }
  componentDidUpdate() {
    document.getElementById("div2").innerHTML =
      "The updated favorite food is " + this.state.favoritefood;
  }
  render() {
    return (
      <div>
        <h1>My Favorite Food is {this.state.favoritefood}</h1>
        <div id="div1"></div>
        <div id="div2"></div>
      </div>
    );
  }
}

ReactDOM.render(<Header />, document.getElementById("root"));
```

This is a React component called `Header` that renders a heading and a button that, when clicked, shows the user's favorite food. The component also has a state that keeps track of the favorite food and whether or not to show it.

The `constructor` method sets the component's initial state, including the default favorite food of "rice" and the `showFavFood` state variable to `false`.

The `componentDidMount` method is called after the component has been mounted to the DOM. In this case, it sets a timeout that will change the favorite food to "pizza" after one second.

The `getSnapshotBeforeUpdate` method is called right before the component is updated. It checks if the `favoriteFood` state variable has changed since the last update and returns an object with the previous favorite food if it has. Otherwise, it returns `null`.

The `componentDidUpdate` method is called after the component has been updated. It receives the previous props, state, and snapshot as arguments. In this case, it checks if the snapshot is not null and logs the previous favorite food to the console.

In the `render` method, the component renders a heading that displays the current favorite food state variable. When the button is clicked, the showFavFood state variable is set to `true` and a paragraph is rendered that displays the current favorite food state variable.

Finally, the `ReactDOM.render` function is called to render the Header component inside an HTML element with the id of "root".

## Component Unmounting Phase

The unmounting phase refers to the lifecycle stage when a component is being removed from the DOM (Document Object Model) and is no longer rendered or accessible.

During this phase, React performs a series of cleanup operations to ensure that the component and its associated resources are properly disposed of.

The unmounting phase is the last stage in the lifecycle of a React component and occurs when the component is being removed from the DOM tree.

This can happen for various reasons, such as when the component is no longer needed, the parent component is re-rendered without including the child component, or when the application is navigating to a different page or view.

### The `componentWillUnmount()` lifecycle method

During the unmounting phase, React calls the following lifecycle methods in order:

- `componentWillUnmount()`: This method is called just before the component is removed from the DOM. It allows you to perform any necessary cleanup, such as canceling timers, removing event listeners, or clearing any data structures that were set up during the mounting phase.
- After `componentWillUnmount()` is called, the component is removed from the DOM and all of its state and props are destroyed.

It's important to note that once a component is unmounted, it cannot be mounted again. If you need to render the component again, you will need to create a new instance of it.

Here's an example of how you might use the `componentWillUnmount()` method to perform cleanup:

```jsx
import React, { Component } from "react";
import ReactDOM from "react-dom";

class MyComponent extends Component {
  state = {
    showChild: true,
  };

  handleDelete = () => {
    this.setState({ showChild: false });
  };

  render() {
    const { showChild } = this.state;

    return (
      <div>
        {showChild && <Child />}
        <button type="button" onClick={this.handleDelete}>
          Delete Header
        </button>
      </div>
    );
  }
}

class Child extends Component {
  componentWillUnmount() {
    alert("The component named Child is about to be unmounted.");
  }

  render() {
    return <h1>Hello World!</h1>;
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<MyComponent />, rootElement);
```

This is a React component that renders a `MyComponent` with a `Child` component that will be conditionally rendered based on the value of `showChild` state.

When the user clicks the "Delete Header" button, the `handleDelete` function will be called which will update the `showChild` state to `false`. This causes the `Child` component to unmount and trigger the `componentWillUnmount` lifecycle method, which will display an alert message.

The `MyComponent` class extends the `Component` class provided by React and defines a state variable `showChild` with an initial value of `true`. It also defines a function `handleDelete` that will be called when the user clicks the "Delete Header" button. This function updates the `showChild` state to `false`.

In the render method of  `MyComponent`, the `showChild` state is used to conditionally render the `Child` component using the logical `&&` operator. If `showChild` is `true`, the `Child` component will be rendered. Otherwise, it will not be rendered.

The `Child` class extends the `Component` class and defines a `componentWillUnmount` method that will be called just before the component is unmounted. In this case, it displays an alert message.

Finally, the `ReactDOM.render` method is called to render the `MyComponent` component inside the element with the ID "root" in the HTML document.

## Conclusion

In summary, React components have a lifecycle consisting of three phases: Mounting, Updating, and Unmounting. Each phase has specific lifecycle methods that are called at different points in the component's lifecycle.

Understanding these lifecycle methods can help developers to control the component's behavior and perform specific actions at different stages of its lifecycle.
