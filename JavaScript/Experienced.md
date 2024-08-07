## JavaScript Interview Questions for Experienced

### 1\. What are arrow functions?

Arrow functions were introduced in the ES6 version of javascript. They provide us with a new and shorter syntax for declaring functions. Arrow functions can only be used as a function expression.

Let’s compare the normal function declaration and the arrow function declaration in detail:

```javascript
// Traditional Function Expression
var add = function (a, b) {
  return a + b;
};

// Arrow Function Expression
var arrowAdd = (a, b) => a + b;
```

Arrow functions are declared without the function keyword. If there is only one returning expression then we don’t need to use the return keyword as well in an arrow function as shown in the example above. Also, for functions having just one line of code, curly braces { } can be omitted.

```javascript
// Traditional function expression
var multiplyBy2 = function (num) {
  return num * 2;
};
// Arrow function expression
var arrowMultiplyBy2 = (num) => num * 2;
```

If the function takes in only one argument, then the parenthesis () around the parameter can be omitted as shown in the code above.

```javascript
var obj1 = {
  valueOfThis: function () {
    return this;
  },
};
var obj2 = {
  valueOfThis: () => {
    return this;
  },
};

obj1.valueOfThis(); // Will return the object obj1
obj2.valueOfThis(); // Will return window/global object
```

The biggest difference between the traditional function expression and the arrow function are:

#### 1\. No `arguments` object in arrow functions

A normal function has an `arguments` object which you can access in the function:

```js
function print() {
  console.log(arguments);
}
```

The `arguments` object is a local variable that contains the arguments passed to the function when called. Let's try it out:

```js
print("hello", 400, false);

// {
//   '0': 'hello',
//   '1': 400,
//   '2': false
// }
```

As you can see here, the three arguments passed when calling `print()` are contained in the `arguments` object which we log to the console. We can access the first argument with `arguments[0]`, the second with `arguments[1]` and the third with `arguments[2]`

But this object does not exist in arrow functions. Let's try it out. Say we have `print` using an arrow function:

```js
const print = () => {
  console.log(arguments);
};

print("hello", 400, false);
// Uncaught ReferenceError: arguments is not defined
```

Now we have a reference error: **arguments is not defined**. That's because the `arguments` variable does not exist in arrow functions.

#### 2\. Arrow functions do not create their own `this` binding

In normal functions, a `this` variable is created which references the objects that call them. For example:

```js
const obj = {
  name: "deeecode",
  age: 200,
  print: function () {
    console.log(this);
  },
};

obj.print();
// {
//   name: 'deeecode',
//   age: 200,
//   print: [Function: print]
// }
```

As you can see here, the `this` in the `print` method points to `obj`, which is the object that calls the method.

Here's another example:

```js
const obj = {
  name: "deeecode",
  age: 200,
  print: function () {
    function print2() {
      console.log(this);
    }

    print2();
  },
};

obj.print();
// Window
```

Here, we have two functions. The first one is `print` which is a method of the `obj` object. The second is `print2` which is a function declared inside `print`. `print2()` is also called directly.

In this case, `print` is called by `obj` (`obj.print()`) but no object calls `print2` (`print2()`). So the `this` in `print2` would reference the window object by default.

Now let's see what happens with an arrow function.

```js
const obj = {
  name: "deeecode",
  age: 200,
  print: () => {
    console.log(this);
  },
};

obj.print();
// Window
```

By using an arrow function for `print`, this function does not automatically create a `this` variable. As a result, any reference to `this` would point to what `this` was before the function was created.

As you see in the result, `this` was pointing to the `Window` object before `print` was created.

Let's see another example:

```js
const obj = {
  name: "deeecode",
  age: 200,
  print: function () {
    const print2 = () => {
      console.log(this);
    };

    print2();
  },
};

obj.print();
// {
//   name: 'deeecode',
//   age: 200,
//   print: [Function: print]
// }
```

Here, we have `print` as a normal function which means a `this` variable is automatically created in it. Then we have `print2` which is an arrow function.

Because `obj` is calling `print` (as in `obj.print()`), the `this` in `print` would point to `obj`.

Since `print2` is an arrow function, it doesn't create its own `this` variable. Therefore, any reference to `this` would point to what the value of `this` was before the function was created. In this case where `obj` calls `print`, `this` was pointing to `obj` before `print2` was created. As you can see in the results, by logging `this` from `print2`, `obj` is the result.

You can learn more about [`this` in my article here](https://dillionmegida.com/p/this-demystified/)

#### 3\. Arrow functions cannot be used as constructors

With normal functions, you can create constructors which serve as a special function for instantiating an object from a class.

Here is an example of an `Animal` class which we instantiate two objects from:

```js
class Animal {
  constructor(name, numOfLegs) {
    this.name = name;
    this.numOfLegs = numOfLegs;
  }

  sayName() {
    console.log(`My name is ${this.name}`);
  }
}

const Dog = new Animal("Bingo", 4);
const Bird = new Animal("Steer", 2);

Dog.sayName();
// My name is Bingo

Bird.sayName();
// My name is Steer
```

Here, we have the `Animal` constructor which can be instantiated with different parameters. In the constructor, two arguments are required: `name` and `noOfLegs`.

In the case of `Dog`, we create a new instance of `Animal` using "Bingo" as the `name` and **4** as the `noOfLegs`.

In the case of `Bird`, we create a new instance of `Animal` using "Steer" as the `name` and **2** as the `noOfLegs`.

By calling `sayName` on `Dog` and `Bird`, you can see how the method works currently with each object. The `this` variable points to the objects and the `name` field is gotten from each of them.

The `this` variable is very important for classes and constructors. In point 2, we saw that arrow functions cannot create their own `this`. For this reason, arrow functions also cannot be used as constructors.

Let's attempt it and see what happens:

```js
class Animal {
  constructor = (name, numOfLegs) => {
    this.name = name;
    this.numOfLegs = numOfLegs;
  };

  sayName() {
    console.log(`My name is ${this.name}`);
  }
}

// Uncaught SyntaxError: Classes may not have a field named 'constructor'
```

Here, we have an arrow function used for the `constructor`. But, we get a SyntaxError: **Classes may not have a field named 'constructor'**.

Because arrow functions involve expressions that are assigned variables, JavaScript now sees `constructor` as a field. And in classes, you cannot have a field named `constructor` as that is a reserved name.

But, we can use arrow functions for the methods in the class without getting errors. For example:

```js
class Animal {
  constructor(name, numOfLegs) {
    this.name = name;
    this.numOfLegs = numOfLegs;
  }

  sayName = () => {
    console.log(`My name is ${this.name}`);
  };
}

const Dog = new Animal("Bingo", 4);

Dog.sayName();
// My name is Bingo
```

Here, we have a normal function for the `constructor`, and an arrow function for the `sayName` method. `sayName` is a field. And we do not get errors.

By calling `sayName()` on `Dog`, we still get "My name is Bingo". Though `sayName` as an arrow function does not create its own `this`, remember that any reference to `this` would point to the value of it before the arrow function was created. In this case, the value of `this` pointed to `Dog` before `sayName` was created.

#### 4\. Arrow functions cannot be declared

When it comes to functions, you need to understand **function declaration** and **function expression**.

Function declarations involve the `function` keyword and a name for the function. For example:

```js
function printHello() {
  console.log("hello");
}
```

`printHello` is a **declared function**. But, check out this example:

```js
const printHello = function () {
  console.log("hello");
};
```

In this case, `printHello` is not a declared function. We have an anonymous function (not named) on the right side of the assignment operator. This function is a **function expression**, which is assigned to the `printHello` variable.

Though the `function` keyword is used, there is no name assigned, which makes it an expression and not a declaration. To prove that it is not a declaration, try the following:

```js
function() {
 console.log("hello")
}
```

Because this expression is not assigned to a variable, you get an error: **SyntaxError: Function statements require a function name**

Back to arrow functions. Normal functions can be declared when you use the function keyword and a name, but arrow functions cannot be declared. They can only be expressed because they are anonymous:

```js
const printHello = () => {
  console.log("hello");
};
```

As you see here, we have an anonymous function (starting from `() => ...`) which is assigned to the `printHello` variable. `printHello` is not a declared function here. It is a variable that holds the evaluated value from the function expression.

#### 5 Arrow functions cannot be accessed before initialization

Hoisting is a concept where a variable or function is lifted to the top of its global or local scope before the whole code is executed. This makes it possible for such a variable/function to be accessed before initialization. Here's a function example:

```js
printName();

console.log("hello");

function printName() {
  console.log("i am dillion");
}

// i am dillion
// hello
```

As you can see here, we called `printName` before it was actually declared in the code. But we don't get any errors. `printName()` is executed (logging "i am dillion" to the console) before `console.log("hello")`.

What happens here is hoisting.

The `printName` function is raised to the top of the global scope (the scope it is declared in) before the whole code is executed, thereby making it possible to execute the function earlier.

But not all kinds of functions can be accessed before initialization. All functions and variables in JavaScript are hoisted, but **only declared functions can be accessed before initialization**.

Here's an example with an arrow function:

```js
printName();

console.log("hello");

const printName = () => {
  console.log("i am dillion");
};

// ReferenceError: Cannot access 'printName' before initialization
```

Running this code, you get an error: **ReferenceError: Cannot access 'printName' before initialization**.

As we saw in point 4, `printName` is not a declared function. It is a variable, declared with `const` which is assigned a function expression. Variables declared with `let` and `const` are hoisted, but they cannot be accessed before the line they are initialized.

Let's say we use `var` for our arrow function:

```js
printName();

console.log("hello");

var printName = () => {
  console.log("i am dillion");
};

// TypeError: printName is not a function
```

Here, we have declared the `printName` variable with `var`. The error we get now is **TypeError: printName is not a function**. The reason for this is that variables declared with `var` are hoisted and accessible, but they have a default value of `undefined`. So attempting to access `printName` before the line it was initialized with the function expression is interpreted as `undefined()`, and as you know, "undefined is not a function".

### 2\. What do mean by prototype design pattern?

The Prototype Pattern produces different objects, but instead of returning uninitialized objects, it produces objects that have values replicated from a template – or sample – object. Also known as the Properties pattern, the Prototype pattern is used to create prototypes.

The introduction of business objects with parameters that match the database's default settings is a good example of where the Prototype pattern comes in handy. The default settings for a newly generated business object are stored in the prototype object.

The Prototype pattern is hardly used in traditional languages, however, it is used in the development of new objects and templates in JavaScript, which is a prototypal language.

### 3\. Differences between declaring variables using var, let and const.

Before the ES6 version of javascript, only the keyword var was used to declare variables. With the ES6 Version, keywords let and const were introduced to declare variables.

<table><tbody><tr><td>keyword</td><td>const</td><td>let</td><td>var</td></tr><tr><td>global scope</td><td>no</td><td>no</td><td>yes</td></tr><tr><td>function scope</td><td>yes</td><td>yes</td><td>yes</td></tr><tr><td>block scope</td><td>yes</td><td>yes</td><td>no</td></tr><tr><td>can be reassigned</td><td>no</td><td>yes</td><td>yes</td></tr></tbody></table>

**Let’s understand the differences with examples:**

```javascript
var variable1 = 23;

let variable2 = 89;

function catchValues() {
  console.log(variable1);
  console.log(variable2);

  // Both the variables can be accessed anywhere since they are declared in the global scope
}

window.variable1; // Returns the value 23

window.variable2; // Returns undefined
```

- The variables declared with the let keyword in the global scope behave just like the variable declared with the var keyword in the global scope.
- Variables declared in the global scope with var and let keywords can be accessed from anywhere in the code.
- But, there is one difference! Variables that are declared with the var keyword in the global scope are added to the window/global object. Therefore, they can be accessed using window.variableName.  
   Whereas, the variables declared with the let keyword are not added to the global object, therefore, trying to access such variables using window.variableName results in an error.

**var vs let in functional scope**

```javascript
function varVsLetFunction() {
  let awesomeCar1 = "Audi";
  var awesomeCar2 = "Mercedes";
}

console.log(awesomeCar1); // Throws an error
console.log(awesomeCar2); // Throws an error
```

Variables are declared in a functional/local scope using **var** and **let** keywords behave exactly the same, meaning, they cannot be accessed from outside of the scope.

```javascript
{
  var variable3 = [1, 2, 3, 4];
}

console.log(variable3); // Outputs [1,2,3,4]

{
  let variable4 = [6, 55, -1, 2];
}

console.log(variable4); // Throws error

for (let i = 0; i < 2; i++) {
  //Do something
}

console.log(i); // Throws error

for (var j = 0; j < 2; i++) {
  // Do something
}

console.log(j); // Outputs 2
```

- In javascript, a block means the code written inside the curly braces **{}**.
- Variables declared with **var** keyword do not have block scope. It means a variable declared in block scope **{}** with the **var** keyword is the same as declaring the variable in the global scope.
- Variables declared with **let** keyword inside the block scope cannot be accessed from outside of the block.

**Const keyword**

- Variables with the **const** keyword behave exactly like a variable declared with the let keyword with only one difference, **any variable declared with the const keyword cannot be reassigned.**
- Example:

```javascript
const x = { name: "Vivek" };

x = { address: "India" }; // Throws an error

x.name = "Nikhil"; // No error is thrown

const y = 23;

y = 44; // Throws an error
```

In the code above, although we can change the value of a property inside the variable declared with **const** keyword, we cannot completely reassign the variable itself.

### 4\. What is the rest parameter and spread operator?

Both rest parameter and spread operator were introduced in the ES6 version of javascript.

**Rest parameter ( … ):**

- It provides an improved way of handling the parameters of a function.
- Using the rest parameter syntax, we can create functions that can take a variable number of arguments.
- Any number of arguments will be converted into an array using the rest parameter.
- It also helps in extracting all or some parts of the arguments.
- Rest parameters can be used by applying three dots (...) before the parameters.

```javascript
function extractingArgs(...args) {
  return args[1];
}

// extractingArgs(8,9,1); // Returns 9

function addAllArgs(...args) {
  let sumOfArgs = 0;
  let i = 0;
  while (i < args.length) {
    sumOfArgs += args[i];
    i++;
  }
  return sumOfArgs;
}

addAllArgs(6, 5, 7, 99); // Returns 117
addAllArgs(1, 3, 4); // Returns 8
```

**\*\*Note- Rest parameter should always be used at the last parameter of a function:**

```javascript
// Incorrect way to use rest parameter
function randomFunc(a,...args,c){
//Do something
}

// Correct way to use rest parameter
function randomFunc2(a,b,...args){
//Do something
}
```

- **Spread operator (…):** Although the syntax of the spread operator is exactly the same as the rest parameter, the spread operator is used to spreading an array, and object literals. We also use spread operators where one or more arguments are expected in a function call.

```javascript
function addFourNumbers(num1, num2, num3, num4) {
  return num1 + num2 + num3 + num4;
}

let fourNumbers = [5, 6, 7, 8];

addFourNumbers(...fourNumbers);
// Spreads [5,6,7,8] as 5,6,7,8

let array1 = [3, 4, 5, 6];
let clonedArray1 = [...array1];
// Spreads the array into 3,4,5,6
console.log(clonedArray1); // Outputs [3,4,5,6]

let obj1 = { x: "Hello", y: "Bye" };
let clonedObj1 = { ...obj1 }; // Spreads and clones obj1
console.log(obj1);

let obj2 = { z: "Yes", a: "No" };
let mergedObj = { ...obj1, ...obj2 }; // Spreads both the objects and merges it
console.log(mergedObj);
// Outputs {x:'Hello', y:'Bye',z:'Yes',a:'No'};
```

> \*\*\*Note- Key differences between rest parameter and spread operator:
>
> - Rest parameter is used to take a variable number of arguments and turns them into an array while the spread operator takes an array or an object and spreads it
> - Rest parameter is used in function declaration whereas the spread operator is used in function calls.

### 5\. In JavaScript, how many different methods can you make an object?

In JavaScript, there are several ways to declare or construct an object.

1. Object.
2. using Class.
3. create Method.
4. Object Literals.
5. using Function.
6. Object Constructor.

### 6\. What is the use of promises in javascript?

**Promises are used to handle asynchronous operations in javascript.**

Before promises, callbacks were used to handle asynchronous operations. But due to the limited functionality of callbacks, using multiple callbacks to handle asynchronous code can lead to unmanageable code.

Promise object has four states -

- Pending - Initial state of promise. This state represents that the promise has neither been fulfilled nor been rejected, it is in the pending state.
- Fulfilled - This state represents that the promise has been fulfilled, meaning the async operation is completed.
- Rejected - This state represents that the promise has been rejected for some reason, meaning the async operation has failed.
- Settled - This state represents that the promise has been either rejected or fulfilled.

A promise is created using the **Promise** constructor which takes in a callback function with two parameters, **resolve** and **reject** respectively.

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/003/414/original/promise.png?1654854623)

**resolve** is a function that will be called when the async operation has been successfully completed.

**reject** is a function that will be called, when the async operation fails or if some error occurs.

Example of a promise:

**Promises are used to handle asynchronous operations like server requests, for ease of understanding, we are using an operation to calculate the sum of three elements.**

In the function below, we are returning a promise inside a function:

```javascript
function sumOfThreeElements(...elements) {
  return new Promise((resolve, reject) => {
    if (elements.length > 3) {
      reject("Only three elements or less are allowed");
    } else {
      let sum = 0;
      let i = 0;
      while (i < elements.length) {
        sum += elements[i];
        i++;
      }
      resolve("Sum has been calculated: " + sum);
    }
  });
}
```

In the code above, we are calculating the sum of three elements, if the length of the elements array is more than 3, a promise is rejected, or else the promise is resolved and the sum is returned.

We can consume any promise by attaching then() and catch() methods to the consumer.

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/003/416/original/Image-08.png?1654857201)

**then()** method is used to access the result when the promise is fulfilled.

**catch()** method is used to access the result/error when the promise is rejected. In the code below, we are consuming the promise:

```javascript
sumOfThreeElements(4, 5, 6)
  .then((result) => console.log(result))
  .catch((error) => console.log(error));
// In the code above, the promise is fulfilled so the then() method gets executed

sumOfThreeElements(7, 0, 33, 41)
  .then((result) => console.log(result))
  .catch((error) => console.log(error));
// In the code above, the promise is rejected hence the catch() method gets executed
```

### 7\. What are classes in javascript?

Introduced in the ES6 version, classes are nothing but syntactic sugars for constructor functions. They provide a new way of declaring constructor functions in javascript.  Below are the examples of how classes are declared and used:

```javascript
// Before ES6 version, using constructor functions
function Student(name, rollNumber, grade, section) {
  this.name = name;
  this.rollNumber = rollNumber;
  this.grade = grade;
  this.section = section;
}

// Way to add methods to a constructor function
Student.prototype.getDetails = function () {
  return "Name: ${this.name}, Roll no: ${this.rollNumber}, Grade: ${this.grade}, Section:${this.section}";
};

let student1 = new Student("Vivek", 354, "6th", "A");
student1.getDetails();
// Returns Name: Vivek, Roll no:354, Grade: 6th, Section:A

// ES6 version classes
class Student {
  constructor(name, rollNumber, grade, section) {
    this.name = name;
    this.rollNumber = rollNumber;
    this.grade = grade;
    this.section = section;
  }

  // Methods can be directly added inside the class
  getDetails() {
    return "Name: ${this.name}, Roll no: ${this.rollNumber}, Grade:${this.grade}, Section:${this.section}";
  }
}

let student2 = new Student("Garry", 673, "7th", "C");
student2.getDetails();
// Returns Name: Garry, Roll no:673, Grade: 7th, Section:C
```

Key points to remember about classes:

- Unlike functions, classes are not hoisted. A class cannot be used before it is declared.
- A class can inherit properties and methods from other classes by using the extend keyword.
- All the syntaxes inside the class must follow the strict mode(‘use strict’) of javascript. An error will be thrown if the strict mode rules are not followed.

### 8\. What are generator functions?

Introduced in the ES6 version, generator functions are a special class of functions.

**They can be stopped midway and then continue from where they had stopped.**

Generator functions are declared with the **function\*** keyword instead of the normal **function** keyword:

```javascript
function* genFunc() {
  // Perform operation
}
```

In normal functions, we use the **return** keyword to return a value and as soon as the return statement gets executed, the function execution stops:

```javascript
function normalFunc() {
  return 22;
  console.log(2); // This line of code does not get executed
}
```

In the case of generator functions, when called, they do not execute the code, instead, they return a **generator object**. This generator object handles the execution.

```javascript
function* genFunc() {
  yield 3;
  yield 4;
}
genFunc(); // Returns Object [Generator] {}
```

The generator object consists of a method called **next()**, this method when called, executes the code until the nearest **yield** statement, and returns the yield value.

For example, if we run the next() method on the above code:

```javascript
genFunc().next(); // Returns {value: 3, done:false}
```

As one can see the next method returns an object consisting of a **value** and **done** properties.  Value property represents the yielded value. Done property tells us whether the function code is finished or not. (Returns true if finished).

Generator functions are used to return iterators. Let’s see an example where an iterator is returned:

```javascript
function* iteratorFunc() {
  let count = 0;
  for (let i = 0; i < 2; i++) {
    count++;
    yield i;
  }
  return count;
}

let iterator = iteratorFunc();
console.log(iterator.next()); // {value:0,done:false}
console.log(iterator.next()); // {value:1,done:false}
console.log(iterator.next()); // {value:2,done:true}
```

As you can see in the code above, the last line returns **done:true**, since the code reaches the return statement.

### 9\. Explain WeakSet in javascript.

In javascript, a Set is a collection of unique and ordered elements. Just like Set, WeakSet is also a collection of unique and ordered elements with some key differences:

- Weakset contains only objects and no other type.
- An object inside the weakset is referenced weakly. This means, that if the object inside the weakset does not have a reference, it will be garbage collected.
- Unlike Set, WeakSet only has three methods, **add()** , **delete()** and **has()** .

```javascript
const newSet = new Set([4, 5, 6, 7]);
console.log(newSet); // Outputs Set {4,5,6,7}

const newSet2 = new WeakSet([3, 4, 5]); //Throws an error

let obj1 = { message: "Hello world" };
const newSet3 = new WeakSet([obj1]);
console.log(newSet3.has(obj1)); // true
```

### 10\. Why do we use callbacks?

A callback function is a method that is sent as an input to another function (now let us name this other function "thisFunction"), and it is performed inside the thisFunction after the function has completed execution.

JavaScript is a scripting language that is based on events. Instead of waiting for a reply before continuing, JavaScript will continue to run while monitoring for additional events. Callbacks are a technique of ensuring that a particular code does not run until another code has completed its execution.

### 11\. Explain WeakMap in javascript.

In javascript, Map is used to store key-value pairs. The key-value pairs can be of both primitive and non-primitive types. WeakMap is similar to Map with key differences:

- The keys and values in weakmap should always be an object.
- If there are no references to the object, the object will be garbage collected.

```javascript
const map1 = new Map();
map1.set("Value", 1);

const map2 = new WeakMap();
map2.set("Value", 2.3); // Throws an error

let obj = { name: "Vivek" };
const map3 = new WeakMap();
map3.set(obj, { age: 23 });
```

### 12\. What is Object Destructuring?

Object destructuring is a new way to extract elements from an object or an array.

- **Object destructuring:** Before ES6 version:

```javascript
const classDetails = {
  strength: 78,
  benches: 39,
  blackBoard: 1,
};

const classStrength = classDetails.strength;
const classBenches = classDetails.benches;
const classBlackBoard = classDetails.blackBoard;
```

The same example using object destructuring:

```javascript
const classDetails = {
  strength: 78,
  benches: 39,
  blackBoard: 1,
};

const {
  strength: classStrength,
  benches: classBenches,
  blackBoard: classBlackBoard,
} = classDetails;

console.log(classStrength); // Outputs 78
console.log(classBenches); // Outputs 39
console.log(classBlackBoard); // Outputs 1
```

As one can see, using object destructuring we have extracted all the elements inside an object in one line of code. If we want our new variable to have the same name as the property of an object we can remove the colon:

```javascript
const { strength: strength } = classDetails;
// The above line of code can be written as:
const { strength } = classDetails;
```

- **Array destructuring:** Before ES6 version:

```javascript
const arr = [1, 2, 3, 4];
const first = arr[0];
const second = arr[1];
const third = arr[2];
const fourth = arr[3];
```

The same example using object destructuring:

```javascript
const arr = [1, 2, 3, 4];
const [first, second, third, fourth] = arr;
console.log(first); // Outputs 1
console.log(second); // Outputs 2
console.log(third); // Outputs 3
console.log(fourth); // Outputs 4
```

### 13\. Difference between prototypal and classical inheritance

Programers build objects, which are representations of real-time entities, in traditional OO programming. Classes and objects are the two sorts of abstractions. A class is a generalization of an object, whereas an object is an abstraction of an actual thing. A Vehicle, for example, is a specialization of a Car. As a result, automobiles (class) are descended from vehicles (object).

Classical inheritance differs from prototypal inheritance in that classical inheritance is confined to classes that inherit from those remaining classes, but prototypal inheritance allows any object to be cloned via an object linking method. Despite going into too many specifics, a prototype essentially serves as a template for those other objects, whether they extend the parent object or not.

### 14\. What is a Temporal Dead Zone?

Temporal Dead Zone is a behaviour that occurs with variables declared using **let** and **const** keywords. It is a behaviour where we try to access a variable before it is initialized. Examples of temporal dead zone:

```javascript
x = 23; // Gives reference error

let x;

function anotherRandomFunc() {
  message = "Hello"; // Throws a reference error

  let message;
}
anotherRandomFunc();
```

In the code above, both in the global scope and functional scope, we are trying to access variables that have not been declared yet. This is called the **Temporal Dead Zone**.

### 15\. What do you mean by JavaScript Design Patterns?

JavaScript design patterns are repeatable approaches for errors that arise sometimes when building JavaScript browser applications. They truly assist us in making our code more stable.

They are divided mainly into 3 categories

1. Creational Design Pattern
2. Structural Design Pattern
3. Behavioral Design Pattern.

- **Creational Design Pattern:** The object generation mechanism is addressed by the JavaScript Creational Design Pattern. They aim to make items that are appropriate for a certain scenario.
- **Structural Design Pattern:** The JavaScript Structural Design Pattern explains how the classes and objects we've generated so far can be combined to construct bigger frameworks. This pattern makes it easier to create relationships between items by defining a straightforward way to do so.
- **Behavioral Design Pattern:** This design pattern highlights typical patterns of communication between objects in JavaScript. As a result, the communication may be carried out with greater freedom.

### 16\. Is JavaScript a pass-by-reference or pass-by-value language?

The variable's data is always a reference for objects, hence it's always pass by value. As a result, if you supply an object and alter its members inside the method, the changes continue outside of it. It appears to be pass by reference in this case. However, if you modify the values of the object variable, the change will not last, demonstrating that it is indeed passed by value.

### 17\. Difference between Async/Await and Generators usage to achieve the same functionality.

- Generator functions are run by their generator yield by yield which means one output at a time, whereas Async-await functions are executed sequentially one after another.
- Async/await provides a certain use case for Generators easier to execute.
- The output result of the Generator function is always value: X, done: Boolean, but the return value of the Async function is always an assurance or throws an error.

### 18\. What are the primitive data types in JavaScript?

A primitive is a data type that isn't composed of other data types. It's only capable of displaying one value at a time. By definition, every primitive is a built-in data type (the compiler must be knowledgeable of them) nevertheless, not all built-in datasets are primitives. In JavaScript, there are 5 different forms of basic data. The following values are available:

1. Boolean
2. Undefined
3. Null
4. Number
5. String

### 19\. What is the role of deferred scripts in JavaScript?

The processing of HTML code while the page loads are disabled by nature till the script hasn't halted. Your page will be affected if your network is a bit slow, or if the script is very hefty. When you use Deferred, the script waits for the HTML parser to finish before executing it. This reduces the time it takes for web pages to load, allowing them to appear more quickly.

### 20\. What has to be done in order to put Lexical Scoping into practice?

To support lexical scoping, a JavaScript function object's internal state must include not just the function's code but also a reference to the current scope chain.

### 21\. What is the purpose of the following JavaScript code?

```javascript
var scope = "global scope";
function check() {
  var scope = "local scope";
  function f() {
    return scope;
  }
  return f;
}
```

Every executing function, code block, and script as a whole in JavaScript has a related object known as the Lexical Environment. The preceding code line returns the value in scope.
