### 1\. How to perform automatic redirect after login?

The react-router package will provide the component `<Redirect>` in React Router. Rendering of a `<Redirect>` component will navigate to a newer location. In the history stack, the current location will be overridden by the new location just like the server-side redirects.

```plaintext
import React, { Component } from 'react'
import { Redirect } from 'react-router'
export default class LoginDemoComponent extends Component {
 render() {
   if (this.state.isLoggedIn === true) {
     return <Redirect to="/your/redirect/page" />
   } else {
     return <div>{'Please complete login'}</div>
   }
 }
}
```

### Conclusion

React has got more popularity among the top IT companies like Facebook, PayPal, Instagram, Uber, etc., around the world especially in India. Hooks is becoming a trend in the React community as it removes the state management complexities.

This article includes the most frequently asked ReactJS and React Hooks interview questions and answers that will help you in interview preparations. Also, remember that your success during the interview is not all about your technical skills, it will also be based on your state of mind and the good impression that you will make at first. All the best!!

### 2\. How to pass data between sibling components using React router?

Passing data between sibling components of React is possible using React Router with the help of `history.push` and `match.params`.

In the code given below, we have a Parent component `AppDemo.js` and have two Child Components `HomePage` and `AboutPage`. Everything is kept inside a Router by using React-router Route. It is also having a route for `/about/{params}` where we will pass the data.

```plaintext
import React, { Component } from ‘react’;
class AppDemo extends Component {
render() {
  return (
    <Router>
      <div className="AppDemo">
      <ul>
        <li>
          <NavLink to="/"  activeStyle={{ color:'blue' }}>Home</NavLink>
        </li>
        <li>
          <NavLink to="/about"  activeStyle={{ color:'blue' }}>About
 </NavLink>
        </li>
 </ul>
             <Route path="/about/:aboutId" component={AboutPage} />
             <Route path="/about" component={AboutPage} />
             <Route path="/" component={HomePage} />
      </div>
    </Router>
  );
}
}
export default AppDemo;
```

The HomePage is a functional component with a button. On button click, we are using `props.history.push(‘/about/’ + data)` to programmatically navigate into `/about/data`.

```plaintext
export default function HomePage(props) {
 const handleClick = (data) => {
  props.history.push('/about/' + data);
 }
return (
  <div>
    <button onClick={() => handleClick('DemoButton')}>To About</button>
  </div>
)
}
```

Also, the functional component AboutPage will obtain the data passed by `props.match.params.aboutId`.

```plaintext
export default function AboutPage(props) {
if(!props.match.params.aboutId) {
    return <div>No Data Yet</div>
}
return (
  <div>
    {`Data obtained from HomePage is ${props.match.params.aboutId}`}
  </div>
)
}
```

After button click in the HomePage the page will look like below:

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/002/333/original/How_to_pass_data_between_sibling_components_using_React_router.png?1640091322)

### 3\. How to re-render the view when the browser is resized?

It is possible to listen to the resize event in **componentDidMount()** and then update the width and height dimensions. It requires the removal of the event listener in the **componentWillUnmount()** method.

Using the below-given code, we can render the view when the browser is resized.

```plaintext
class WindowSizeDimensions extends React.Component {
 constructor(props){
   super(props);
   this.updateDimension = this.updateDimension.bind(this);
 }

 componentWillMount() {
   this.updateDimension()
 }
 componentDidMount() {
   window.addEventListener('resize', this.updateDimension)
 }
 componentWillUnmount() {
   window.removeEventListener('resize', this.updateDimension)
 }
 updateDimension() {
   this.setState({width: window.innerWidth, height: window.innerHeight})
 }
 render() {
   return <span>{this.state.width} x {this.state.height}</span>
 }
}
```

### 4\. How to create a switching component for displaying different pages?

A switching component refers to a component that will render one of the multiple components. We should use an object for mapping prop values to components.

A below-given example will show you how to display different pages based on page prop using switching component:

```plaintext
import HomePage from './HomePage'
import AboutPage from './AboutPage'
import FacilitiesPage from './FacilitiesPage'
import ContactPage from './ContactPage'
import HelpPage from './HelpPage'
const PAGES = {
 home: HomePage,
 about: AboutPage,
 facilitiess: FacilitiesPage,
 contact: ContactPage
 help: HelpPage
}
const Page = (props) => {
 const Handler = PAGES[props.page] || HelpPage
 return <Handler {...props} />
}
// The PAGES object keys can be used in the prop types for catching errors during dev-time.
Page.propTypes = {
 page: PropTypes.oneOf(Object.keys(PAGES)).isRequired
}
```

### 5\. Explain how to create a simple React Hooks example program.

I will assume that you are having some coding knowledge about JavaScript and have installed Node on your system for creating a below given React Hook program. An installation of Node comes along with the command-line tools: npm and npx, where npm is useful to install the packages into a project and npx is useful in running commands of Node from the command line. The npx looks in the current project folder for checking whether a command has been installed there. When the command is not available on your computer, the npx will look in the npmjs.com repository, then the latest version of the command script will be loaded and will run without locally installing it. This feature is useful in creating a skeleton React application within a few key presses.

Open the Terminal inside the folder of your choice, and run the following command:

```plaintext
npx create-react-app react-items-with-hooks
```

Here, the `create-react-app` is an app initializer created by Facebook, to help with the easy and quick creation of React application, providing options to customize it while creating the application? The above command will create a new folder named react-items-with-hooks and it will be initialized with a basic React application. Now, you will be able to open the project in your favourite IDE. You can see an src folder inside the project along with the main application component `App.js`. This file is having a single function `App()` which will return an element and it will make use of an extended JavaScript syntax(JSX) for defining the component.

JSX will permit you for writing HTML-style template syntax directly into the JavaScript file. This mixture of JavaScript and HTML will be converted by React toolchain into pure JavaScript that will render the HTML element.

It is possible to define your own React components by writing a function that will return a JSX element. You can try this by creating a new file `src/SearchItem.js`and put the following code into it.

```plaintext
import React from 'react';
export function SearchItem() {
 return (
   <div>
     <div className="search-input">
       <input type="text" placeholder="SearchItem"/>
     </div>
     <h1 className="h1">Search Results</h1>
     <div className="items">
       <table>
         <thead>
           <tr>
             <th className="itemname-col">Item Name</th>
             <th className="price-col">Price</th>
             <th className="quantity-col">Quantity</th>
           </tr>
         </thead>
         <tbody></tbody>
       </table>
     </div>
   </div>
 );
}
```

This is all about how you can create a component. It will only display the empty table and doesn’t do anything. But you will be able to use the Search component in the application. Open the file `src/App.js` and add the import statement given below to the top of the file.

```plaintext
import { SearchItem } from './SearchItem';
```

Now, from the logo.svg, import will be removed and then contents of returned value in the function `App()` will be replaced with the following code:

```plaintext
<div className="App">
 <header>
   Items with Hooks
 </header>
 <SearchItem/>
</div>
```

You can notice that the element <SearchItem/> has been used just similar to an HTML element. The JSX syntax will enable for including the components in this approach directly within the JavaScript code. Your application can be tested by running the below-given command in your terminal.

`npm start`

This command will compile your application and open your default browser into [http://localhost:4000](http://localhost:4000/). This command can be kept on running when code development is in progress to make sure that the application is up-to-date, and also this browser page will be reloaded each time you modify and save the code.

This application will work finely, but it doesn’t look nice as it doesn’t react to any input from the user. You can make it more interactive by adding a state with React Hooks, adding authentication, etc.

### 6\. Explain conditional rendering in React.

Conditional rendering refers to the dynamic output of user interface markups based on a condition state. It works in the same way as JavaScript conditions. Using conditional rendering, it is possible to toggle specific application functions, API data rendering, hide or show elements, decide permission levels, authentication handling, and so on.

There are different approaches for implementing conditional rendering in React. Some of them are:

- Using if-else conditional logic which is suitable for smaller as well as for medium-sized applications
- Using ternary operators, which takes away some amount of complication from if-else statements
- Using element variables, which will enable us to write cleaner code.

### 7\. Can React Hook replaces Redux?

The React Hook cannot be considered as a replacement for Redux (It is an open-source, JavaScript library useful in managing the application state) when it comes to the management of the global application state tree in large complex applications, even though the React will provide a useReducer hook that manages state transitions similar to Redux. Redux is very useful at a lower level of component hierarchy to handle the pieces of a state which are dependent on each other, instead of a declaration of multiple useState hooks.

In commercial web applications which is larger, the complexity will be high, so using only React Hook may not be sufficient. Few developers will try to tackle the challenge with the help of React Hooks and others will combine React Hooks with the Redux.

### 8\. What is React Router?

React Router refers to the standard library used for routing in React. It permits us for building a single-page web application in React with navigation without even refreshing the page when the user navigates. It also allows to change the browser URL and will keep the user interface in sync with the URL. React Router will make use of the component structure for calling the components, using which appropriate information can be shown. Since React is a component-based framework, it’s not necessary to include and use this package. Any other compatible routing library would also work with React.

The major components of React Router are given below:

- **BrowserRouter:** It is a router implementation that will make use of the HTML5 history API (pushState, popstate, and event replaceState) for keeping your UI to be in sync with the URL. It is the parent component useful in storing all other components.
- **Routes:** It is a newer component that has been introduced in the React v6 and an upgrade of the component.
- **Route:** It is considered to be a conditionally shown component and some UI will be rendered by this whenever there is a match between its path and the current URL.
- **Link:** It is useful in creating links to various routes and implementing navigation all over the application. It works similarly to the anchor tag in HTML.

### 9\. Do Hooks cover all the functionalities provided by the classes?

Our goal is for Hooks to cover all the functionalities for classes at its earliest. There are no Hook equivalents for the following methods that are not introduced in Hooks yet:

- `getSnapshotBeforeUpdate()`
- `getDerivedStateFromError()`
- `componentDidCatch()`

Since it is an early time for Hooks, few third-party libraries may not be compatible with Hooks at present, but they will be added soon.

### 10\. How does the performance of using Hooks will differ in comparison with the classes?

- React Hooks will avoid a lot of overheads such as the instance creation, binding of events, etc., that are present with classes.
- Hooks in React will result in smaller component trees since they will be avoiding the nesting that exists in HOCs (Higher Order Components) and will render props which result in less amount of work to be done by React.

### 11\. Differentiate React Hooks vs Classes.

| React Hooks                                                                         | Classes                                                                                                       |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| It is used in functional components of React.                                       | It is used in class-based components of React.                                                                |
| It will not require a declaration of any kind of constructor.                       | It is necessary to declare the constructor inside the class component.                                        |
| It does not require the use of `this` keyword in state declaration or modification. | Keyword `this` will be used in state declaration (`this.state`) and in modification (`this.setState()`).      |
| It is easier to use because of the `useState` functionality.                        | No specific function is available for helping us to access the state and its corresponding setState variable. |
| React Hooks can be helpful in implementing Redux and context API.                   | Because of the long setup of state declarations, class states are generally not preferred.                    |

### 12\. Explain about types of Hooks in React.

There are two types of Hooks in React. They are:

**1\. Built-in Hooks:** The built-in Hooks are divided into 2 parts as given below:

- **Basic Hooks:**
  - `useState()`: This functional component is used to set and retrieve the state.
  - `useEffect()`: It enables for performing the side effects in the functional components.
  - `useContext()`: It is used for creating common data that is to be accessed by the components hierarchy without having to pass the props down to each level.
- **Additional Hooks:**
  - `useReducer()` : It is used when there is a complex state logic that is having several sub-values or when the upcoming state is dependent on the previous state. It will also enable you to optimization of component performance that will trigger deeper updates as it is permitted to pass the dispatch down instead of callbacks.
  - `useMemo()` : This will be used for recomputing the memoized value when there is a change in one of the dependencies. This optimization will help for avoiding expensive calculations on each render.
  - `useCallback()` : This is useful while passing callbacks into the optimized child components and depends on the equality of reference for the prevention of unneeded renders.
  - `useImperativeHandle()`:  It will enable modifying the instance that will be passed with the ref object.
  - `useDebugValue()`: It is used for displaying a label for custom hooks in React DevTools.
  - `useRef()` : It will permit creating a reference to the DOM element directly within the functional component.
  - `useLayoutEffect()`: It is used for the reading layout from the DOM and re-rendering synchronously.

**2\. Custom Hooks:** A custom Hook is basically a function of JavaScript. The Custom Hook working is similar to a regular function. The “use” at the beginning of the Custom Hook Name is required for React to understand that this is a custom Hook and also it will describe that this specific function follows the rules of Hooks. Moreover, developing custom Hooks will enable you for extracting component logic from within reusable functions.

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/002/331/original/types_of_Hooks_in_React.png?1640091273)

### 13\. Does React Hook work with static typing?

Static typing refers to the process of code check during the time of compilation for ensuring all variables will be statically typed. React Hooks are functions that are designed to make sure about all attributes must be statically typed. For enforcing stricter static typing within our code, we can make use of the React API with custom Hooks.

### 14\. What are the lifecycle methods of React?

React lifecycle hooks will have the methods that will be automatically called at different phases in the component lifecycle and thus it provides good control over what happens at the invoked point. It provides the power to effectively control and manipulate what goes on throughout the component lifecycle.

For example, if you are developing the YouTube application, then the application will make use of a network for buffering the videos and it consumes the power of the battery (assume only these two). After playing the video if the user switches to any other application, then you should make sure that the resources like network and battery are being used most efficiently. You can stop or pause the video buffering which in turn stops the battery and network usage when the user switches to another application after video play.

So we can say that the developer will be able to produce a quality application with the help of lifecycle methods and it also helps developers to make sure to plan what and how to do it at different points of birth, growth, or death of user interfaces.

The various lifecycle methods are:

- `constructor()`: This method will be called when the component is initiated before anything has been done. It helps to set up the initial state and initial values.
- `getDerivedStateFromProps()`: This method will be called just before element(s) rendering in the DOM. It helps to set up the state object depending on the initial props. The getDerivedStateFromProps() method will have a state as an argument and it returns an object that made changes to the state. This will be the first method to be called on an updating of a component.
- `render()`: This method will output or re-render the HTML to the DOM with new changes. The render() method is an essential method and will be called always while the remaining methods are optional and will be called only if they are defined.
- `componentDidMount()`: This method will be called after the rendering of the component. Using this method, you can run statements that need the component to be already kept in the DOM.
- `shouldComponentUpdate()`: The Boolean value will be returned by this method which will specify whether React should proceed further with the rendering or not. The default value for this method will be True.
- `getSnapshotBeforeUpdate()`: This method will provide access for the props as well as for the state before the update. It is possible to check the previously present value before the update, even after the update.
- `componentDidUpdate()`: This method will be called after the component has been updated in the DOM.
- `componentWillUnmount()`: This method will be called when the component removal from the DOM is about to happen.

### 15\. What are the different phases of the component lifecycle?

There are four different phases in the lifecycle of React component. They are:

- **Initialization:** During this phase, React component will prepare by setting up the default props and initial state for the upcoming tough journey.
- **Mounting:** Mounting refers to putting the elements into the browser DOM. Since React uses VirtualDOM, the entire browser DOM which has been currently rendered would not be refreshed. This phase includes the lifecycle methods `componentWillMount` and `componentDidMount`.
- **Updating:** In this phase, a component will be updated when there is a change in the state or props of a component. This phase will have lifecycle methods like `componentWillUpdate`, `shouldComponentUpdate`, `render`, and `componentDidUpdate`.
- **Unmounting:** In this last phase of the component lifecycle, the component will be removed from the DOM or will be unmounted from the browser DOM. This phase will have the lifecycle method named `componentWillUnmount`.

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/002/330/original/different_phases_of_the_component_lifecycle.png?1640091214)

### 16\. What are Higher Order Components?

Simply put, Higher-Order Component(HOC) is a function that takes in a component and returns a new component.

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/002/339/original/Higher_Order_Components.png?1640091703)

**When do we need a Higher Order Component?**

While developing React applications, we might develop components that are quite similar to each other with minute differences. In most cases, developing similar components might not be an issue but, while developing larger applications we need to keep our code **DRY**, therefore, we want an **abstraction** that allows us to define this logic in a single place and share it across components. HOC allows us to create that abstraction.

**Example of a HOC:**

Consider the following components having similar functionality. The following component displays the list of articles:

```plaintext
// "GlobalDataSource" is some global data source
class ArticlesList extends React.Component {
 constructor(props) {
   super(props);
   this.handleChange = this.handleChange.bind(this);
   this.state = {
     articles: GlobalDataSource.getArticles(),
   };
 }
 componentDidMount() {
   // Listens to the changes added
   GlobalDataSource.addChangeListener(this.handleChange);
 }
 componentWillUnmount() {
   // Listens to the changes removed
   GlobalDataSource.removeChangeListener(this.handleChange);
 }
 handleChange() {
   // States gets Update whenver data source changes
   this.setState({
     articles: GlobalDataSource.getArticles(),
   });
 }
 render() {
   return (
     <div>
       {this.state.articles.map((article) => (
         <ArticleData article={article} key={article.id} />
       ))}
     </div>
   );
 }
}
```

The following component displays the list of users:

```plaintext
// "GlobalDataSource" is some global data source
class UsersList extends React.Component {
 constructor(props) {
   super(props);
   this.handleChange = this.handleChange.bind(this);
   this.state = {
     users: GlobalDataSource.getUsers(),
   };
 }
 componentDidMount() {
   // Listens to the changes added
   GlobalDataSource.addChangeListener(this.handleChange);
 }
 componentWillUnmount() {
   // Listens to the changes removed
   GlobalDataSource.removeChangeListener(this.handleChange);
 }
 handleChange() {
   // States gets Update whenver data source changes
   this.setState({
     users: GlobalDataSource.getUsers(),
   });
 }
 render() {
   return (
     <div>
       {this.state.users.map((user) => (
         <UserData user={user} key={user.id} />
       ))}
     </div>
   );
 }
}
```

Notice the above components, both have similar functionality but, they are calling different methods to an API endpoint.

Let’s create a Higher Order Component to create an abstraction:

```plaintext
// Higher Order Component which takes a component
// as input and returns another component
// "GlobalDataSource" is some global data source
function HOC(WrappedComponent, selectData) {
 return class extends React.Component {
   constructor(props) {
     super(props);
     this.handleChange = this.handleChange.bind(this);
     this.state = {
       data: selectData(GlobalDataSource, props),
     };
   }
   componentDidMount() {
     // Listens to the changes added
     GlobalDataSource.addChangeListener(this.handleChange);
   }
   componentWillUnmount() {
     // Listens to the changes removed
     GlobalDataSource.removeChangeListener(this.handleChange);
   }
   handleChange() {
     this.setState({
       data: selectData(GlobalDataSource, this.props),
     });
   }
   render() {
     // Rendering the wrapped component with the latest data data
     return <WrappedComponent data={this.state.data} {...this.props} />;
   }
 };
}
```

We know HOC is a function that takes in a component and returns a component.

In the code above, we have created a function called HOC which returns a component and performs functionality that can be shared across both the **ArticlesList** component and **UsersList** Component.

The second parameter in the HOC function is the function that calls the method on the API endpoint.

We have reduced the duplicated code of the **componentDidUpdate** and **componentDidMount** functions.

Using the concept of Higher-Order Components, we can now render the **ArticlesList** and **UsersList** components in the following way:

```plaintext
const ArticlesListWithHOC = HOC(ArticlesList, (GlobalDataSource) => GlobalDataSource.getArticles());
const UsersListWithHOC = HOC(UsersList, (GlobalDataSource) => GlobalDataSource.getUsers());
```

Remember, we are not trying to change the functionality of each component, we are trying to share a single functionality across multiple components using HOC.

### 17\. How to pass data between react components?

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/002/338/original/How_to_pass_data_between_react_components.png?1640091660)

**Parent Component to Child Component (using props)**

With the help of props, we can send data from a parent to a child component.

**How do we do this?**

Consider the following Parent Component:

```plaintext
import ChildComponent from "./Child";
   function ParentComponent(props) {
    let [counter, setCounter] = useState(0);

    let increment = () => setCounter(++counter);

    return (
      <div>
        <button onClick={increment}>Increment Counter</button>
        <ChildComponent counterValue={counter} />
      </div>
    );
   }
```

As one can see in the code above, we are rendering the child component inside the parent component, by providing a prop called counterValue. The value of the counter is being passed from the parent to the child component.

We can use the data passed by the parent component in the following way:

```plaintext
function ChildComponent(props) {
return (
  <div>
    <p>Value of counter: {props.counterValue}</p>
  </div>
);
}
```

We use the **props.counterValue** to display the data passed on by the parent component.

**Child Component to Parent Component (using callbacks)**

This one is a bit tricky. We follow the steps below:

- Create a callback in the parent component which takes in the data needed as a parameter.
- Pass this callback as a prop to the child component.
- Send data from the child component using the callback.

We are considering the same example above but in this case, we are going to pass the updated counterValue from child to parent.

**Step1 and Step2:** Create a callback in the parent component, pass this callback as a prop.

```plaintext
function ParentComponent(props) {
let [counter, setCounter] = useState(0);
let callback = valueFromChild => setCounter(valueFromChild);
return (
  <div>
    <p>Value of counter: {counter}</p>
    <ChildComponent callbackFunc={callback} counterValue={counter} />
  </div>
);
}
```

As one can see in the code above, we created a function called callback which takes in the data received from the child component as a parameter.

Next, we passed the function callback as a prop to the child component.

**Step3:** Pass data from the child to the parent component.

```plaintext
function ChildComponent(props) {
let childCounterValue = props.counterValue;
return (
  <div>
    <button onClick={() => props.callbackFunc(++childCounterValue)}>
      Increment Counter
    </button>
  </div>
);
}
```

In the code above, we have used the props.counterValue and set it to a variable called childCounterValue.

Next, on button click, we pass the incremented childCounterValue to the **props.callbackFunc**.

This way, we can pass data from the child to the parent component.

### 18\. Name a few techniques to optimize React app performance.

There are many ways through which one can optimize the performance of a React app, let’s have a look at some of them:

- **Using useMemo( )** -
  - It is a React hook that is used for caching CPU-Expensive functions.
  - Sometimes in a React app, a CPU-Expensive function gets called repeatedly due to re-renders of a component, which can lead to slow rendering.  
     useMemo( ) hook can be used to cache such functions. By using useMemo( ), the CPU-Expensive function gets called only when it is needed.
- **Using React.PureComponent -**
  - It is a base component class that checks the state and props of a component to know whether the component should be updated.
  - Instead of using the simple React.Component, we can use React.PureComponent to reduce the re-renders of a component unnecessarily.
- **Maintaining State Colocation -**
  - This is a process of moving the state as close to where you need it as possible.
  - Sometimes in React app, we have a lot of unnecessary states inside the parent component which makes the code less readable and harder to maintain. Not to forget, having many states inside a single component leads to unnecessary re-renders for the component.
  - It is better to shift states which are less valuable to the parent component, to a separate component.
- **Lazy Loading -**
  - It is a technique used to reduce the load time of a React app. Lazy loading helps reduce the risk of web app performances to a minimum.

### 19\. What are the different ways to style a React component?

There are many different ways through which one can style a React component. Some of the ways are :

- **Inline Styling:** We can directly style an element using inline style attributes. Make sure the value of style is a JavaScript object:

```plaintext
class RandomComponent extends React.Component {
 render() {
   return (
     <div>
       <h3 style={{ color: "Yellow" }}>This is a heading</h3>
       <p style={{ fontSize: "32px" }}>This is a paragraph</p>
     </div>
   );
 }
}
```

- **Using JavaScript object:** We can create a separate JavaScript object and set the desired style properties. This object can be used as the value of the inline style attribute.

```plaintext
class RandomComponent extends React.Component {
 paragraphStyles = {
   color: "Red",
   fontSize: "32px"
 };

 headingStyles = {
   color: "blue",
   fontSize: "48px"
 };

 render() {
   return (
     <div>
       <h3 style={this.headingStyles}>This is a heading</h3>
       <p style={this.paragraphStyles}>This is a paragraph</p>
     </div>
   );
 }
}
```

- **CSS Stylesheet:** We can create a separate CSS file and write all the styles for the component inside that file. This file needs to be imported inside the component file.

```plaintext
import './RandomComponent.css';

class RandomComponent extends React.Component {
 render() {
   return (
     <div>
       <h3 className="heading">This is a heading</h3>
       <p className="paragraph">This is a paragraph</p>
     </div>
   );
 }
}
```

- **CSS Modules:** We can create a separate CSS module and import this module inside our component. Create a file with “.module.css”‘ extension, styles.module.css:

```plaintext
.paragraph{
 color:"red";
 border:1px solid black;
}
```

We can import this file inside the component and use it:

```plaintext
import styles from  './styles.module.css';

class RandomComponent extends React.Component {
 render() {
   return (
     <div>
       <h3 className="heading">This is a heading</h3>
       <p className={styles.paragraph} >This is a paragraph</p>
     </div>
   );
 }
}
```

### 20\. How to prevent re-renders in React?

- **Reason for re-renders in React:**
  - Re-rendering of a component and its child components occur when props or the state of the component has been changed.
  - Re-rendering components that are not updated, affects the performance of an application.
- **How to prevent re-rendering:**

Consider the following components:

```plaintext
class Parent extends React.Component {
state = { messageDisplayed: false };
componentDidMount() {
  this.setState({ messageDisplayed: true });
}
render() {
  console.log("Parent is getting rendered");
  return (
    <div className="App">
      <Message />
    </div>
  );
}
}
class Message extends React.Component {
constructor(props) {
  super(props);
  this.state = { message: "Hello, this is vivek" };
}
render() {
  console.log("Message is getting rendered");
  return (
    <div>
      <p>{this.state.message}</p>
    </div>
  );
}
}
```

- The **Parent** component is the parent component and the **Message** is the child component. Any change in the parent component will lead to re-rendering of the child component as well. To prevent the re-rendering of child components, we use the shouldComponentUpdate( ) method:

> \*\*Note- Use shouldComponentUpdate( ) method only when you are sure that it’s a static component.

```plaintext
class Message extends React.Component {
constructor(props) {
  super(props);
  this.state = { message: "Hello, this is vivek" };
}
shouldComponentUpdate() {
  console.log("Does not get rendered");
  return false;
}
render() {
  console.log("Message is getting rendered");
  return (
    <div>
      <p>{this.state.message}</p>
    </div>
  );
}
}
```

As one can see in the code above, we have returned **false** from the shouldComponentUpdate( ) method, which prevents the child component from re-rendering.

### 21\. Explain Strict Mode in React.

StrictMode is a tool added in **version 16.3** of React to highlight potential problems in an application. It performs additional checks on the application.

```plaintext
function App() {
 return (
   <React.StrictMode>
     <div classname="App">
       <Header/>
       <div>
         Page Content
       </div>
       <Footer/>
     </div>
   </React.StrictMode>
 );
}
```

To enable StrictMode, `<React.StrictMode>` tags need to be added inside the application:

```plaintext
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
const rootElement = document.getElementById("root");
ReactDOM.render(
<React.StrictMode>
  <App />
</React.StrictMode>,
rootElement
);
```

StrictMode currently helps with the following issues:

- **Identifying components with unsafe lifecycle methods:**
  - Certain lifecycle methods are unsafe to use in asynchronous react applications. With the use of third-party libraries, it becomes difficult to ensure that certain lifecycle methods are not used.
  - StrictMode helps in providing us with a warning if any of the class components use an unsafe lifecycle method.
- **Warning about the usage of legacy string API:**
  - If one is using an older version of React, **callback ref** is the recommended way to manage **refs** instead of using the **string refs**. StrictMode gives a warning if we are using **string refs** to manage refs.
- **Warning about the usage of findDOMNode:**
  - Previously, findDOMNode( ) method was used to search the tree of a DOM node. This method is deprecated in React. Hence, the StrictMode gives us a warning about the usage of this method.
- **Warning about the usage of legacy context API (because the API is error-prone).**
