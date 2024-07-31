# What are Controlled and Uncontrolled Components in React.js?

In React.js, managing form inputs and user interactions is a crucial part of building dynamic web applications.

Two key concepts that developers need to understand are controlled and uncontrolled components. These concepts define how form data is handled within a React component.

Controlled components rely on React state to manage the form data, while uncontrolled components use the DOM itself to handle form data.

In this article, we will explore the differences between controlled and uncontrolled components, how to implement them, and some best practices for using each approach in your React applications.

## What are Controlled Components?

Controlled components are form elements (like `input`, `textarea`, or `select`) that are managed by React state. This means that the value of the form element is set and updated through React state, making React the "single source of truth" for the form data.

By controlling form elements via state, you gain more control over user interactions and can easily enforce validation, format data, and respond to changes.

Here's an example of a controlled component:

```jsx
import React, { useState } from "react";

function ControlledComponent() {
  const [value, setValue] = useState("");

  const handleChange = (event) => {
    setValue(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert("A name was submitted: " + value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={value} onChange={handleChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

export default ControlledComponent;
```

In this example:

- The `value` state holds the current value of the input field.
- The `handleChange` function updates the state whenever the user types in the input field.
- The `handleSubmit` function handles the form submission, using the current state value.

## How Controlled Components Work

Controlled components in React ensure that the form data is handled by the React state, providing a consistent and predictable way to manage user input.

Here’s a breakdown of how these components work, including state management in the parent component, passing values as props to child components, handling user input with event handlers, and updating state in the parent component.

### State Management in the Parent Component

State management is often handled in the parent component, especially when multiple child components need to interact or share state. The parent component maintains the state and passes it down to child components via props.

```jsx
import React, { useState } from "react";
import ChildComponent from "./ChildComponent";

function ParentComponent() {
  const [inputValue, setInputValue] = useState("");

  return (
    <div>
      <h1>Controlled Component Example</h1>
      <ChildComponent value={inputValue} setValue={setInputValue} />
    </div>
  );
}

export default ParentComponent;
```

### Passing Values as Props to a Child Component

The parent component passes the state value and a state updater function to the child component as props. This allows the child component to display the current state and update it when needed.

```jsx
import React from "react";

function ChildComponent({ value, setValue }) {
  const handleChange = (event) => {
    setValue(event.target.value);
  };

  return (
    <form>
      <label>
        Name:
        <input type="text" value={value} onChange={handleChange} />
      </label>
    </form>
  );
}

export default ChildComponent;
```

### Handling User Input with Event Handlers

Event handlers are used to manage user input. When the user types into the input field, the `onChange` event triggers the `handleChange` function, which updates the state in the parent component.

```jsx
function ChildComponent({ value, setValue }) {
  const handleChange = (event) => {
    setValue(event.target.value);
  };

  return (
    <form>
      <label>
        Name:
        <input type="text" value={value} onChange={handleChange} />
      </label>
    </form>
  );
}
```

### Updating State in a Parent Component

When the state updater function (`setValue`) is called in the child component, it updates the state in the parent component. This causes the parent component to re-render, which in turn re-renders the child component with the new state value.

```jsx
function ParentComponent() {
  const [inputValue, setInputValue] = useState("");

  return (
    <div>
      <h1>Controlled Component Example</h1>
      <ChildComponent value={inputValue} setValue={setInputValue} />
    </div>
  );
}
```

### Putting It All Together

Here's the complete example showing how controlled components work with state management in the parent component:

```jsx
// ParentComponent.jsx
import React, { useState } from 'react';
import ChildComponent from './ChildComponent';

function ParentComponent() {
  const [inputValue, setInputValue] = useState('');

  return (
    <div>
      <h1>Controlled Component Example</h1>
      <ChildComponent value={inputValue} setValue={setInputValue} />
    </div>
  );
}

export default ParentComponent;

// ChildComponent.jsx
import React from 'react';

function ChildComponent({ value, setValue }) {
  const handleChange = (event) => {
    setValue(event.target.value);
  };

  return (
    <form>
      <label>
        Name:
        <input type="text" value={value} onChange={handleChange} />
      </label>
    </form>
  );
}

export default ChildComponent;
```

Controlled components in React provide a good way to manage form data by using React state as the single source of truth. This approach involves managing state in the parent component, passing values and state updater functions as props to child components, handling user input with event handlers, and updating state in the parent component.

This method ensures consistent and predictable form behavior, making it easier to implement validation, conditional rendering, and other interactive features.

## Benefits of Using Controlled Components

Controlled components offer several advantages that can significantly improve the development experience and functionality of React applications. Here are the key benefits:

### Predictable State Management

Using controlled components ensures that the form data is always in sync with the React state. This predictability comes from having a single source of truth for the data, which is the state itself.

Since the state drives the UI, any change in the state immediately reflects in the form elements and vice versa. This makes it easier to debug and understand how data flows through your application.

**Example:**

```jsx
import React, { useState } from "react";

function PredictableForm() {
  const [name, setName] = useState("");

  const handleChange = (event) => {
    setName(event.target.value);
  };

  return (
    <div>
      <input type="text" value={name} onChange={handleChange} />
      <p>Current value: {name}</p>
    </div>
  );
}
```

In this example, the input field and the displayed text are always synchronized, providing a predictable behavior.

### Easier Form Validation

Controlled components make it straightforward to implement form validation. Since the form data is stored in the component state, you can easily validate it before updating the state or on form submission. This approach allows you to provide real-time feedback to users as they interact with the form.

**Example:**

```jsx
import React, { useState } from "react";

function ValidatedForm() {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  const handleChange = (event) => {
    const value = event.target.value;
    setEmail(value);

    if (!value.includes("@")) {
      setError("Invalid email address");
    } else {
      setError("");
    }
  };

  return (
    <div>
      <input type="email" value={email} onChange={handleChange} />
      {error && <p style={{ color: "red" }}>{error}</p>}
    </div>
  );
}
```

Here, the validation logic runs on every change, providing immediate feedback to the user if the input is invalid.

### Integration with Complex UI Libraries

Controlled components integrate seamlessly with complex UI libraries and frameworks, such as Redux for state management or Formik for handling forms.

By managing form data in the component state, you can easily connect your forms to these libraries and benefit from their advanced features like global state management, asynchronous data fetching, and more.

**Example with Formik:**

```jsx
import React from "react";
import { Formik, Form, Field, ErrorMessage } from "formik";
import * as Yup from "yup";

const SignupForm = () => (
  <Formik
    initialValues={{ email: "" }}
    validationSchema={Yup.object({
      email: Yup.string().email("Invalid email address").required("Required"),
    })}
    onSubmit={(values, { setSubmitting }) => {
      setTimeout(() => {
        alert(JSON.stringify(values, null, 2));
        setSubmitting(false);
      }, 400);
    }}
  >
    {({ isSubmitting }) => (
      <Form>
        <label htmlFor="email">Email</label>
        <Field type="email" name="email" />
        <ErrorMessage name="email" component="div" />
        <button type="submit" disabled={isSubmitting}>
          Submit
        </button>
      </Form>
    )}
  </Formik>
);

export default SignupForm;
```

In this example, Formik handles form state and validation, demonstrating how controlled components can be part of more complex setups.

Controlled components provide predictable state management, easier form validation, and seamless integration with complex UI libraries.

By keeping the form data in the React state, you ensure consistency and control over your application's behavior, making it easier to build and maintain interactive and dynamic user interfaces.

## Examples of Controlled Components

Controlled components are fundamental in React for handling form inputs in a predictable and manageable way.

Here are some examples of how you can implement controlled components for various types of form inputs, including text fields, email fields, password fields, select menus, checkboxes, and radio buttons.

### Input Fields (Text, Email, Password)

##### Text Input

```jsx
import React, { useState } from "react";

function TextInput() {
  const [text, setText] = useState("");

  const handleChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <label>
        Text:
        <input type="text" value={text} onChange={handleChange} />
      </label>
      <p>Entered Text: {text}</p>
    </div>
  );
}

export default TextInput;
```

##### Email Input

```jsx
import React, { useState } from "react";

function EmailInput() {
  const [email, setEmail] = useState("");

  const handleChange = (event) => {
    setEmail(event.target.value);
  };

  return (
    <div>
      <label>
        Email:
        <input type="email" value={email} onChange={handleChange} />
      </label>
      <p>Entered Email: {email}</p>
    </div>
  );
}

export default EmailInput;
```

##### Password Input

```jsx
import React, { useState } from "react";

function PasswordInput() {
  const [password, setPassword] = useState("");

  const handleChange = (event) => {
    setPassword(event.target.value);
  };

  return (
    <div>
      <label>
        Password:
        <input type="password" value={password} onChange={handleChange} />
      </label>
      <p>Entered Password: {password}</p>
    </div>
  );
}

export default PasswordInput;
```

#### Select Menus

```jsx
import React, { useState } from "react";

function SelectMenu() {
  const [option, setOption] = useState("option1");

  const handleChange = (event) => {
    setOption(event.target.value);
  };

  return (
    <div>
      <label>
        Choose an option:
        <select value={option} onChange={handleChange}>
          <option value="option1">Option 1</option>
          <option value="option2">Option 2</option>
          <option value="option3">Option 3</option>
        </select>
      </label>
      <p>Selected Option: {option}</p>
    </div>
  );
}

export default SelectMenu;
```

#### Checkboxes

```jsx
import React, { useState } from "react";

function Checkbox() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChange = (event) => {
    setIsChecked(event.target.checked);
  };

  return (
    <div>
      <label>
        Accept Terms:
        <input type="checkbox" checked={isChecked} onChange={handleChange} />
      </label>
      <p>Checked: {isChecked ? "Yes" : "No"}</p>
    </div>
  );
}

export default Checkbox;
```

#### Radio Buttons

```jsx
import React, { useState } from "react";

function RadioButton() {
  const [selectedOption, setSelectedOption] = useState("option1");

  const handleChange = (event) => {
    setSelectedOption(event.target.value);
  };

  return (
    <div>
      <label>
        <input
          type="radio"
          value="option1"
          checked={selectedOption === "option1"}
          onChange={handleChange}
        />
        Option 1
      </label>
      <label>
        <input
          type="radio"
          value="option2"
          checked={selectedOption === "option2"}
          onChange={handleChange}
        />
        Option 2
      </label>
      <label>
        <input
          type="radio"
          value="option3"
          checked={selectedOption === "option3"}
          onChange={handleChange}
        />
        Option 3
      </label>
      <p>Selected Option: {selectedOption}</p>
    </div>
  );
}

export default RadioButton;
```

Controlled components provide a clear and consistent way to handle form inputs in React. By using React state to manage the values of input fields, select menus, checkboxes, and radio buttons, you ensure that the UI remains in sync with the state.

This approach simplifies validation, makes data handling predictable, and facilitates integration with complex UI libraries.

## What are Uncontrolled Components?

Uncontrolled components in React manage their own state internally rather than relying on React state. This approach is useful for simple forms where you don't need to manipulate the input data through React state updates.

**Example:**

```jsx
import React, { Component } from "react";

class UncontrolledComponent extends Component {
  constructor(props) {
    super(props);
    // Create a ref to hold the input DOM element
    this.inputRef = React.createRef();
  }

  handleSubmit = () => {
    // Access the input value using the ref
    console.log(this.inputRef.current.value);
  };

  render() {
    return (
      <div>
        {/* Use ref attribute to attach the ref to the input element */}
        <input type="text" ref={this.inputRef} />
        <button onClick={this.handleSubmit}>Submit</button>
      </div>
    );
  }
}
```

- **Ref Usage:** In uncontrolled components, we use the `ref` attribute to create a reference (`this.inputRef`) to the DOM node of the input field.
- **Handling Input:** When the user enters data and clicks "Submit", `this.inputRef.current.value` allows us to directly access the current value of the input field without involving React state.
- **Advantages:** Uncontrolled components can be simpler and faster for basic form handling. They are often used when the form data is not needed in React state for any processing or validation.

**Key Points:**

- **Internal State:** Uncontrolled components manage their state internally with the help of refs, not with React state updates.
- **Direct DOM Access:** Accessing form data is done directly through DOM refs (`this.inputRef.current.value`).
- **Simplicity:** They are straightforward for simple forms where real-time validation or complex form interactions are not necessary.

Uncontrolled components are handy in scenarios where you want a lightweight approach to handling form data without the overhead of managing state in React.

## How Uncontrolled Components Work

Uncontrolled components manage their state internally using DOM refs (`useRef` hook in functional components or `React.createRef()` in class components) to access form element values directly.

Unlike controlled components, where form data is managed through React state and updated via `setState`, uncontrolled components bypass React's state management for handling form inputs.

### Direct DOM Access with useRef Hook

In functional components, the `useRef` hook allows us to create a mutable reference that persists across renders. We can use this ref to directly access DOM nodes, such as input fields.

**Example:**

```jsx
import React, { useRef } from "react";

function UncontrolledComponent() {
  const inputRef = useRef(null); // Create a ref to hold the input DOM element

  const handleSubmit = () => {
    // Access the input value using the ref
    console.log(inputRef.current.value);
  };

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}

export default UncontrolledComponent;
```

### Accessing an Element's Value on Submit

In the example above:

- **Creating a Ref:** `const inputRef = useRef(null);` initializes a ref named `inputRef` to hold the reference to the input DOM element.
- **Handling Submit:** When the "Submit" button is clicked (`onClick={handleSubmit}`), the `handleSubmit` function retrieves the current value of the input field using `inputRef.current.value`.

**Key Points:**

- **DOM Access:** The `useRef` hook allows direct access to DOM elements, enabling us to interact with them without updating React state.
- **Form Submission:** On form submission (`onClick={handleSubmit}`), the function accesses the current value of the input field through `inputRef.current.value`.
- **Simplicity:** Uncontrolled components are straightforward for basic form handling scenarios where direct DOM manipulation suffices, avoiding the need for managing state updates in React.

Using uncontrolled components with `useRef` is particularly useful for handling forms where real-time validation or complex interactions aren't necessary, focusing instead on simplicity and performance.

## When to Use Uncontrolled Components

Uncontrolled components are ideal in specific scenarios where simplicity and direct DOM manipulation are advantageous over managing state with React.

Here are the key situations when using uncontrolled components is beneficial:

### 1\. Simple Forms with Limited Interactions

Uncontrolled components shine in scenarios where:

- **The Forms Arent' That Complex:** The form is straightforward with minimal input fields and does not require complex validation or dynamic updates based on other form inputs.
- **Performance is Important:** Directly accessing form values via DOM refs (`useRef` or `React.createRef()`) can be more performant than updating React state for each input change, especially in large forms.
- **You want Simplicity:** When you prefer a simpler implementation without managing state updates and re-renders for form inputs.

### 2\. Focus Management (Selecting Text)

In some cases, you might need to manage user interaction such as selecting text within an input field or programmatically focusing on a specific input without triggering React state updates unnecessarily.

Uncontrolled components allow you to:

- **Directly manipulate the DOM:** Use DOM methods like `select()` on the input element directly via refs to manage focus or text selection.
- **Handling focus and text selection directly with refs**: This can be more efficient and straightforward compared to triggering state updates and managing focus state in React components.

#### Example Use Case:

```jsx
import React, { useRef } from "react";

function UncontrolledComponent() {
  const inputRef = useRef(null); // Create a ref to hold the input DOM element

  const handleFocus = () => {
    inputRef.current.select(); // Selects all text in the input field
  };

  return (
    <div>
      <input type="text" ref={inputRef} defaultValue="Initial Value" />
      <button onClick={handleFocus}>Select Text</button>
    </div>
  );
}

export default UncontrolledComponent;
```

In this example, clicking the "Select Text" button calls `inputRef.current.select()` to select all text within the input field directly, without involving React state updates. This is a simple yet effective use of uncontrolled components for managing focus and text selection.

## Limitations of Uncontrolled Components

Using uncontrolled components in React can offer simplicity and performance benefits in certain scenarios, but they also come with limitations that are important to consider:

### Difficulty in Form Validation:

- Uncontrolled components can make form validation more challenging compared to controlled components. Since the form data is managed internally by the DOM rather than React state, validating and ensuring data consistency across multiple inputs can be complex.
- Validation logic often involves accessing and checking each input's value directly through refs (`ref.current.value`). This approach can lead to more manual and error-prone validation code, especially in forms with complex validation requirements.

### Less Predictable State Management:

- Uncontrolled components bypass React's state management, which can lead to less predictable state handling in complex applications. Changes in form data are not automatically synchronized with React's state updates or other component state, potentially leading to inconsistencies.
- This lack of synchronization can make it challenging to maintain a single source of truth for form data across different components or when integrating with other state management solutions like Redux or Context API.

### Limited React Ecosystem Integration:

- Uncontrolled components may not fully leverage React's ecosystem features, such as state persistence, time-travel debugging (with Redux), or seamless integration with third-party libraries designed for controlled components.
- Components relying on React state benefit from these features, enhancing developer productivity and application maintainability.

## Examples of Uncontrolled Components

Uncontrolled components in React are particularly useful for handling input fields and textarea elements where direct DOM manipulation suffices, and React state management isn't necessary.

Here are examples of how uncontrolled components can be applied:

### 1\. Input Fields (Read-only or Pre-filled Data)

Uncontrolled components can be used when you need to display read-only or pre-filled data in an input field without managing its state in React.

**Example:**

```jsx
import React, { useRef } from "react";

function UncontrolledInput() {
  const initialValue = "Hello, World!";
  const inputRef = useRef(null); // Create a ref to hold the input DOM element

  const handleFocus = () => {
    inputRef.current.select(); // Selects all text in the input field on focus
  };

  return (
    <div>
      {/* Using defaultValue for pre-filled data */}
      <input type="text" ref={inputRef} defaultValue={initialValue} readOnly />
      <button onClick={handleFocus}>Select Text</button>
    </div>
  );
}

export default UncontrolledInput;
```

In this example:

- The `defaultValue` attribute sets the initial value of the input field.
- `readOnly` attribute prevents users from editing the input field, making it read-only.
- `useRef` hook manages focus and selection of text within the input field using `inputRef.current`.

### 2\. Textarea Elements

Uncontrolled components are also applicable to textarea elements, especially when dealing with multiline text input where immediate state updates are not necessary.

**Example:**

```jsx
import React, { useRef } from "react";

function UncontrolledTextarea() {
  const initialText =
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit.";
  const textareaRef = useRef(null); // Create a ref to hold the textarea DOM element

  const handleClear = () => {
    textareaRef.current.value = ""; // Clear textarea content directly
  };

  return (
    <div>
      {/* Using defaultValue for pre-filled content */}
      <textarea
        ref={textareaRef}
        defaultValue={initialText}
        rows={4}
        cols={50}
      />
      <button onClick={handleClear}>Clear Text</button>
    </div>
  );
}

export default UncontrolledTextarea;
```

In this example:

- The `defaultValue` attribute sets the initial content of the textarea.
- `useRef` hook manages direct manipulation of textarea content using `textareaRef.current`.
- `rows` and `cols` attributes define the dimensions of the textarea.

**Key points:**

- **Direct DOM Access:** Uncontrolled components leverage `useRef` to directly manipulate DOM elements for managing input fields and textarea content.
- **Performance:** Suitable for scenarios where real-time updates or complex state management aren't required, enhancing performance by avoiding unnecessary state updates.
- **Simplicity:** Provides a straightforward approach to handling form elements with default or read-only values, maintaining simplicity in component logic.

These examples demonstrate how uncontrolled components can handle input fields and textarea elements effectively in React applications, focusing on simplicity and direct DOM manipulation for specific use cases.
