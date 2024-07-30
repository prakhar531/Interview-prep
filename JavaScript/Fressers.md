# JavaScript Interview Questions for Freshers

## 1. What are the different data types present in javascript?

To know the type of a JavaScript variable, we can use the **typeof** operator.

**1.Primitive types**

**String** \- It represents a series of characters and is written with quotes. A string can be represented using a single or a double quote.

Example :

```javascript
var str = "Vivek Singh Bisht"; //using double quotes
var str2 = "John Doe"; //using single quotes
```

- **Number** \- It represents a number and can be written with or without decimals.

Example :

```javascript
var x = 3; //without decimal
var y = 3.6; //with decimal
```

- **BigInt** \- This data type is used to store numbers which are above the limitation of the Number data type. It can store large integers and is represented by adding “n” to an integer literal.

Example :

```javascript
var bigInteger = 234567890123456789012345678901234567890;
```

- **Boolean** \- It represents a logical entity and can have only two values : true or false. Booleans are generally used for conditional testing.

Example :

```javascript
var a = 2;
var b = 3;
var c = 2;
(a == b)(
  // returns false
  a == c
); //returns true
```

- **Undefined** \- When a variable is declared but not assigned, it has the value of undefined and it’s type is also undefined.

Example :

```javascript
var x; // value of x is undefined
var y = undefined; // we can also set the value of a variable as undefined
```

- **Null** \- It represents a non-existent or a invalid value.

Example :

```javascript
var z = null;
```

- **Symbol** \- It is a new data type introduced in the ES6 version of javascript. It is used to store an anonymous and unique value.

Example :

```javascript
var symbol1 = Symbol("symbol");
```

- typeof **of primitive types** :

```javascript
typeof "John Doe"; // Returns "string"
typeof 3.14; // Returns "number"
typeof true; // Returns "boolean"
typeof 234567890123456789012345678901234567890n; // Returns bigint
typeof undefined; // Returns "undefined"
typeof null; // Returns "object" (kind of a bug in JavaScript)
typeof Symbol("symbol"); // Returns Symbol
```

**2\. Non-primitive types**

- Primitive data types can store only a single value. To store multiple and complex values, non-primitive data types are used.
- Object - Used to store collection of data.
- Example:

```javascript
// Collection of data in key-value pairs

var obj1 = {
  x: 43,
  y: "Hello world!",
  z: function () {
    return this.x;
  },
};

// Collection of data as an ordered list

var array1 = [5, "Hello", true, 4.1];
```

> #### **Note- It is important to remember that any data type that is not a primitive data type, is of Object type in javascript.**

![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/mobile/study_plan-bf1728cccc109be1b27549ae18f4571495aaa096b70f313c8232292849f9b07c.svg.gz) ![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/desktop/study_plan-fb58ec94dd27940f470d62dee6d85c8161f6afc2b9dcbced18278212ce50b8b9.svg.gz)

Create a free personalised study plan Create a FREE custom study plan

Get into your dream companies with expert guidance

Get into your dream companies with expert..

![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/code-99b8ddab28469d3e18187c7e7f62dcf921ece612e63043b7515547d441ea3ebb.svg.gz) Real-Life Problems

![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/suitcase-7129128344fb59d27c28914ce39a52b40df37b3da954c23330359726019a8fb7.svg.gz) Prep for Target Roles

![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/pencil-aaf6423aa93927b3965ae3006bc88653f14fee9586297e82fa1153ab475c8459.svg.gz) Custom Plan Duration

![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/calendar-blank-fd5b0a13bc91a3876224b83db892e456e05f669a469dbe4f3d62a6600836c79c.svg.gz) Flexible Plans

[Create My Plan ![](https://assets.interviewbit.com/assets/ibpp/interview_guides/assets/arrow-right-54a813c1b9b6df712c72a314c89081e5a96674ee7ee6454dd7c063d0fe79bb1c.svg.gz)](https://www.interviewbit.com/interview-preparation-kit/)

### 2\. Explain Hoisting in javascript.

Hoisting is the default behaviour of javascript where all the variable and function declarations are moved on top.

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/003/406/original/Hoisting.png?1654851517)

This means that irrespective of where the variables and functions are declared, they are moved on top of the scope. The scope can be both local and global.

**Example 1:**

```javascript
hoistedVariable = 3;
console.log(hoistedVariable); // outputs 3 even when the variable is declared after it is initialized
var hoistedVariable;
```

**Example 2:**

```javascript
hoistedFunction(); // Outputs " Hello world! " even when the function is declared after calling

function hoistedFunction() {
  console.log(" Hello world! ");
}
```

**Example 3:**

```javascript
// Hoisting takes place in the local scope as well
function doSomething() {
  x = 33;
  console.log(x);
  var x;
}
```

doSomething(); // Outputs 33 since the local variable “x” is hoisted inside the local scope

> #### **Note - Variable initializations are not hoisted, only variable declarations are hoisted:**

```javascript
var x;
console.log(x); // Outputs "undefined" since the initialization of "x" is not hoisted
x = 23;
```

> #### **Note - To avoid hoisting, you can run javascript in strict mode by using “use strict” on top of the code:**

```javascript
"use strict";
x = 23; // Gives an error since 'x' is not declared
var x;
```

### 3\. Why do we use the word “debugger” in javascript?

The debugger for the browser must be activated in order to debug the code. Built-in debuggers may be switched on and off, requiring the user to report faults. The remaining section of the code should stop execution before moving on to the next line while debugging.

You can download a PDF version of Javascript Interview Questions.

![](https://assets.interviewbit.com/assets/ibpp/interview_guides/download_v2-f7bcad529b2845c93dddc78cd31acf9ecb098c42854a1757f0f8949950377c02.svg.gz)Download PDF[![](https://assets.interviewbit.com/assets/ibpp/interview_guides/download_v2-f7bcad529b2845c93dddc78cd31acf9ecb098c42854a1757f0f8949950377c02.svg.gz)Download PDF](<javascript:void(0)>)

### Download PDF

---

Your requested download is ready!  
Click here to download.

### 4\. Difference between “ == “ and “ === “ operators.

Both are comparison operators. The difference between both the operators is that “==” is used to compare values whereas, “ === “ is used to compare both values and types.

**Example:**

```javascript
var x = 2;
var y = "2";
(x == y)(
  // Returns true since the value of both x and y is the same
  x === y
); // Returns false since the typeof x is "number" and typeof y is "string"
```

### 5\. Difference between var and let keyword in javascript.
