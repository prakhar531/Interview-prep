## JavaScript Coding Interview Questions

### 1\. What is the output of the following code?

```javascript
const b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

for (let i = 0; i < 10; i++) {
  setTimeout(() => console.log(b[i]), 1000);
}

for (var i = 0; i < 10; i++) {
  setTimeout(() => console.log(b[i]), 1000);
}
```

**Ans.**

```javascript
1;
2;
3;
4;
5;
6;
7;
8;
9;
10;
undefined;
undefined;
undefined;
undefined;
undefined;
undefined;
undefined;
undefined;
undefined;
undefined;
```

### Conclusion

It is preferable to keep the JavaScript, CSS, and HTML in distinct Separate 'javascript' files. Dividing the code and HTML sections will make them easier to understand and deal with. This strategy is also simpler for several programmers to use at the same time. JavaScript code is simple to update. Numerous pages can utilize the same group of JavaScript Codes. If we utilize External JavaScript scripts and need to alter the code, we must do it just once. So that we may utilize a number and maintain it much more easily. Remember that professional experience and expertise are only one aspect of recruitment. Previous experience and personal skills are both vital in landing (or finding the ideal applicant for the job.

Remember that many JavaScript structured interviews are free and have no one proper answer. Interviewers would like to know why you answered the way you did, not if you remembered the answer. Explain your answer process and be prepared to address it. If you're looking to further enhance your JavaScript skills, consider enrolling in this free JavaScript course by [Scaler Topics](https://www.scaler.com/topics/course/javascript-beginners/) to gain hands-on experience and improve your problem-solving abilities.

### 2\. In JavaScript, how do you turn an Object into an Array \[\]?

```javascript
let obj = { id: "1", name: "user22", age: "26", work: "programmer" };

//Method 1: Convert the keys to Array using - Object.keys()
console.log(Object.keys(obj));
// ["id", "name", "age", "work"]

// Method 2 Converts the Values to Array using - Object.values()
console.log(Object.values(obj));
// ["1", "user22r", "26", "programmer"]

// Method 3 Converts both keys and values using - Object.entries()
console.log(Object.entries(obj));
//[["id", "1"],["name", "user22"],["age", "26"],["work", “programmer"]]
```

### 3\. Write the code to find the vowels

```javascript
const findVowels = (str) => {
  let count = 0;
  const vowels = ["a", "e", "i", "o", "u"];
  for (let char of str.toLowerCase()) {
    if (vowels.includes(char)) {
      count++;
    }
  }
  return count;
};
```

### 4\. Write the code given If two strings are anagrams of one another, then return true.

```javascript
var firstWord = "Deepak";
var secondWord = "Aman";

isAnagram(wordOne, wordTwo); // true

function isAnagram(one, two) {
  //Change both words to lowercase for case insensitivity..
  var a = one.toLowerCase();
  var b = two.toLowerCase();

  // Sort the strings, then combine the array to a string. Examine the outcomes.
  a = a.split("").sort().join("");
  b = b.split("").sort().join("");

  return a === b;
}
```

### 5\. Write the code for dynamically inserting new components.

```plaintext
<html>
<head>
<title>inserting new components dynamically</title>
<script type="text/javascript">
    function addNode () { var newP = document. createElement("p");
    var textNode = document.createTextNode(" This is other node");
    newP.appendChild(textNode); document.getElementById("parent1").appendChild(newP); }
</script>
</head>
<body> <p id="parent1">firstP<p> </body>
</html>
```

### 6\. Implement a function that returns an updated array with r right rotations on an array of integers a .

**Example:**

Given the following array: **\[2,3,4,5,7\]**  
Perform **3** right rotations:  
First rotation : \[7,2,3,4,5\] , Second rotation : \[5,7,2,3,4\] and, Third rotation: \[4,5,7,2,3\]

return **\[4,5,7,2,3\]**

**Answer:**

```plaintext
function rotateRight(arr,rotations){
  if(rotations == 0) return arr;
  for(let i = 0; i < rotations;i++){
    let element = arr.pop();
    arr.unshift(element);
  }
  return arr;
}
rotateRight([2, 3, 4, 5, 7], 3); // Return [4,5,7,2,3]
rotateRight([44, 1, 22, 111], 5); // Returns [111,44,1,22]
```

### 7\. Write a function that performs binary search on a sorted array.

```javascript
function binarySearch(arr,value,startPos,endPos){
  if(startPos > endPos) return -1;

  let middleIndex = Math.floor(startPos+endPos)/2;

  if(arr[middleIndex] === value) return middleIndex;

  elsif(arr[middleIndex] > value){
    return binarySearch(arr,value,startPos,middleIndex-1);
  }
  else{
    return binarySearch(arr,value,middleIndex+1,endPos);
  }
}    
```

### 8\. Guess the outputs of the following code:

#### **\*\*Note - Code 2 and Code 3 require you to modify the code, instead of guessing the output.**

```javascript
// Code 1

(function (a) {
  return (function () {
    console.log(a);
    a = 23;
  })();
})(45);

// Code 2

// Each time bigFunc is called, an array of size 700 is being created,
// Modify the code so that we don't create the same array again and again

function bigFunc(element) {
  let newArray = new Array(700).fill("♥");
  return newArray[element];
}

console.log(bigFunc(599)); // Array is created
console.log(bigFunc(670)); // Array is created again

// Code 3

// The following code outputs 2 and 2 after waiting for one second
// Modify the code to output 0 and 1 after one second.

function randomFunc() {
  for (var i = 0; i < 2; i++) {
    setTimeout(() => console.log(i), 1000);
  }
}
randomFunc();
```

**Answers -**

**Code 1** \- Outputs **45**.

Even though a is defined in the outer function, due to closure the inner functions have access to it.

**Code 2** \- This code can be modified by using closures,

```javascript
function bigFunc() {
  let newArray = new Array(700).fill("♥");
  return (element) => newArray[element];
}

let getElement = bigFunc(); // Array is created only once
getElement(599);
getElement(670);
```

**Code 3** \- Can be modified in two ways:

Using **let** keyword:

```javascript
function randomFunc() {
  for (let i = 0; i < 2; i++) {
    setTimeout(() => console.log(i), 1000);
  }
}
randomFunc();
```

**Using closure:**

```javascript
function randomFunc() {
  for (var i = 0; i < 2; i++) {
    (function (i) {
      setTimeout(() => console.log(i), 1000);
    })(i);
  }
}
randomFunc();
```

### 9\. Guess the outputs of the following code:

```plaintext
// Code 1

  let hero = {
    powerLevel: 99,
    getPower(){
      return this.powerLevel;
    }
  }

  let getPower = hero.getPower;

  let hero2 = {powerLevel:42};
  console.log(getPower());
  console.log(getPower.apply(hero2));



  // Code 2

  const a = function(){
    console.log(this);

    const b = {
      func1: function(){
        console.log(this);
      }
    }

    const c = {
      func2: ()=>{
        console.log(this);
      }
    }

    b.func1();
    c.func2();
  }

  a();



  // Code 3

  const b = {
    name:"Vivek",
    f: function(){
      var self = this;
      console.log(this.name);
      (function(){
        console.log(this.name);
        console.log(self.name);
      })();
    }
  }
  b.f();
```

Answers:

**Code 1** \- Output in the following order:

```plaintext
undefined
42
```

Reason - The first output is **undefined** since when the function is invoked, it is invoked referencing the global object:

```plaintext
window.getPower() = getPower();
```

**Code 2** \- Outputs in the following order:

```plaintext
global/window object
object "b"
global/window object
```

Since we are using the arrow function inside **func2, this** keyword refers to the global object.

**Code 3** \- Outputs in the following order:

```plaintext
"Vivek"
undefined
"Vivek"
```

Only in the IIFE inside the function **f**, **this** keyword refers to the global/window object.



### 10\. Guess the output of the following code:

```javascript
var x = 23;

(function () {
  var x = 43;
  (function random() {
    x++;
    console.log(x);
    var x = 21;
  })();
})();
```

### Answer:

Output is **NaN**.

random() function has functional scope since x is declared and hoisted in the functional scope.

Rewriting the random function will give a better idea about the output:

```javascript
function random() {
  var x; // x is hoisted
  x++; // x is not a number since it is not initialized yet
  console.log(x); // Outputs NaN
  x = 21; // Initialization of x
}
```

### 11\. Guess the outputs of the following code:

```javascript
// Code 1:

let x = {},
  y = { name: "Ronny" },
  z = { name: "John" };
x[y] = { name: "Vivek" };
x[z] = { name: "Akki" };
console.log(x[y]);

// Code 2:

function runFunc() {
  console.log("1" + 1);
  console.log("A" - 1);
  console.log(2 + "-2" + "2");
  console.log("Hello" - "World" + 78);
  console.log("Hello" + "78");
}
runFunc();

// Code 3:

let a = 0;
let b = false;
console.log(a == b);
console.log(a === b);
```

**Answers:**

**Code 1** \- Output will be **{name: “Akki”}.**

Adding objects as properties of another object should be done carefully.

Writing **x\[y\] = {name:”Vivek”}** , is same as writing **x\[‘object Object’\] = {name:”Vivek”}** ,

While setting a property of an object, **javascript coerces the parameter into a string.**

Therefore, since **y** is an object, it will be converted to **‘object Object’.**

Both x\[y\] and x\[z\] are referencing the same property.

**Code 2** \- Outputs in the following order:

```javascript
11;
Nan;
2 - 22;
NaN;
Hello78;
```

**Code 3** \- Output in the following order due to equality coercion:

```javascript
true;
false;
```

### 12\. Guess the outputs of the following codes:

```javascript
// Code 1:

function func1() {
  setTimeout(() => {
    console.log(x);
    console.log(y);
  }, 3000);

  var x = 2;
  let y = 12;
}
func1();

// Code 2:

function func2() {
  for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 2000);
  }
}
func2();

// Code 3:

(function () {
  setTimeout(() => console.log(1), 2000);
  console.log(2);
  setTimeout(() => console.log(3), 0);
  console.log(4);
})();
```

**Answers:**

- **Code 1** \- Outputs **2** and **12**. Since, even though **let** variables are not hoisted, due to the async nature of javascript, the complete function code runs before the setTimeout function. Therefore, it has access to both x and y.
- **Code 2** \- Outputs **3**, three times since variable declared with **var** keyword does not have block scope. Also, inside the for loop, the variable i is incremented first and then checked.
- **Code 3** \- Output in the following order:

```javascript
2;
4;
3;
1; // After two seconds
```

Even though the second timeout function has a waiting time of zero seconds, the javascript engine always evaluates the setTimeout function using the Web API, and therefore, the complete function executes before the setTimeout function can execute.
