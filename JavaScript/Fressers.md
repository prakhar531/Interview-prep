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

### 6\. Explain Implicit Type Coercion in javascript.

Implicit type coercion in javascript is the automatic conversion of value from one data type to another. It takes place when the operands of an expression are of different data types.

- **String coercion**

String coercion takes place while using the ‘ + ‘ operator. When a number is added to a string, the number type is always converted to the string type.

Example 1:

```javascript
var x = 3;
var y = "3";
x + y; // Returns "33"
```

Example 2:

```javascript
var x = 24;
var y = "Hello";
x + y; // Returns "24Hello";
```

> #### Note - ‘ + ‘ operator when used to add two numbers, outputs a number. The same ‘ + ‘ operator when used to add two strings, outputs the concatenated string:

```javascript
var name = "Vivek";
var surname = " Bisht";
name + surname; // Returns "Vivek Bisht"
```

Let’s understand both the examples where we have added a number to a string,

When JavaScript sees that the operands of the expression x + y are of different types ( one being a number type and the other being a string type ), it converts the number type to the string type and then performs the operation. Since after conversion, both the variables are of string type, the ‘ + ‘ operator outputs the concatenated string “33” in the first example and “24Hello” in the second example.

> #### Note - Type coercion also takes place when using the ‘ - ‘ operator, but the difference while using ‘ - ‘ operator is that, a string is converted to a number and then subtraction takes place.

```javascript
var x = 3;
Var y = "3";
x - y    //Returns 0 since the variable y (string type) is converted to a number type
```

- **Boolean Coercion**

Boolean coercion takes place when using logical operators, ternary operators, if statements, and loop checks. To understand boolean coercion in if statements and operators, we need to understand truthy and falsy values.

Truthy values are those which will be converted (coerced) to **true**. Falsy values are those which will be converted to **false**.

All values except **false, 0, 0n, -0, “”, null, undefined, and NaN** are truthy values.

**If statements:**

Example:

```javascript
var x = 0;
var y = 23;

if (x) {
  console.log(x);
} // The code inside this block will not run since the value of x is 0(Falsy)

if (y) {
  console.log(y);
} // The code inside this block will run since the value of y is 23 (Truthy)
```

- **Logical operators:**

Logical operators in javascript, unlike operators in other programming languages, **do not return true or false. They always return one of the operands.**

**OR ( | | ) operator** \- If the first value is truthy, then the first value is returned. Otherwise, always the second value gets returned.

**AND ( && ) operator** \- If both the values are truthy, always the second value is returned. If the first value is falsy then the first value is returned or if the second value is falsy then the second value is returned.

Example:

```javascript
var x = 220;
var y = "Hello";
var z = undefined;

x | | y    // Returns 220 since the first value is truthy

x | | z   // Returns 220 since the first value is truthy

x && y    // Returns "Hello" since both the values are truthy

y && z   // Returns undefined since the second value is falsy

if( x && y ){
  console.log("Code runs" ); // This block runs because x && y returns "Hello" (Truthy)
}

if( x || z ){
  console.log("Code runs");  // This block runs because x || y returns 220(Truthy)
}
```

- **Equality Coercion**

Equality coercion takes place when using ‘ == ‘ operator. As we have stated before

**The ‘ == ‘ operator compares values and not types.**

While the above statement is a simple way to explain == operator, it’s not completely true

The reality is that while using the ‘==’ operator, coercion takes place.

The ‘==’ operator, converts both the operands to the same type and then compares them.

Example:

```javascript
var a = 12;
var b = "12";
a == b; // Returns true because both 'a' and 'b' are converted to the same type and then compared. Hence the operands are equal.
```

Coercion does not take place when using the ‘===’ operator. Both operands are not converted to the same type in the case of ‘===’ operator.

Example:

```javascript
var a = 226;
var b = "226";

a === b; // Returns false because coercion does not take place and the  operands are of different types. Hence they are not equal.
```

### 7\. Is javascript a statically typed or a dynamically typed language?

JavaScript is a dynamically typed language. In a dynamically typed language, the type of a variable is checked during **run-time** in contrast to a statically typed language, where the type of a variable is checked during **compile-time.**

![](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/003/407/original/static_vs_dynamic.png?1654852333)

Since javascript is a loosely(dynamically) typed language, variables in JS are not associated with any type. A variable can hold the value of any data type.

For example, a variable that is assigned a number type can be converted to a string type:

```javascript
var a = 23;
var a = "Hello World!";
```
