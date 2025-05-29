# JavaScript
## DataTypes & Variables
- **premetive**: Number, String, Boolean, Undefined, Null, Symbol, BigInt
- **NonPremetive**: Object, Array, Function
# Let , Var, Const: 
**Basically those are keywords**
 ## Let:
 - **Block Scope** : only accessible within the block, statement, or expression where they are defined.
 ```js
 if (true) {
    let x = 10;
    console.log(x); // Output: 10
}
console.log(x); // ReferenceError: x is not defined
```
- **Re-declaration Error**:
```js
let z = 30;
let z = 40; // SyntaxError: Identifier 'z' has already been declared
```
- **No issue in hoisting** : While variables declared with let are hoisted, they are not initialized. This creates a temporal dead zone (TDZ) where accessing the variable before its declaration results in a ReferenceError, helping prevent unintended access.
```js
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 20;
```
- **TDZ**:TDZ behavior ensures that variables are not accessed before they are properly initialized.
- **safe for loops**: loop block scope
```js
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000); // 0 1 2
}
```
- **Safe for closure**: let i = 0; i < 3; i++: You're looping from i = 0 to i = 2.

Inside the loop, you're pushing a function into the funcs array. That function, when called later, will log the value of i.

The key is that let is block-scoped.

In each iteration of the for loop, a new i binding is created — this means the arrow function you push to funcs captures the current value of i in that iteration, not a shared value.
```js
const funcs = [];
for (let i = 0; i < 3; i++) {
    funcs.push(() => console.log(i));
}
funcs[0]();//0
funcs[1]();//1
funcs[2]();//2
```
---
## Var:
- **Function Scope**: This means they are accessible anywhere within the function they are declared, even before their declaration due to hoisting.
```js
function testVar() {
    console.log(x); // undefined
    var x = 10;
    console.log(x); // Output: 10
}

console.log(x); // Error: x is not defined
```
- **Not Block Scope**: See the difference between Func vs Block Scope
```js
if (true) {
    var blockVar = "I am not block scoped";
}
console.log(blockVar); // Output: I am not block scoped
```
- **Global Scope & Global OBJ property**: declear with var makes global ,accessible from any where.
**Also create new key in window object**
```js
var globalVar = "Global";
console.log(window.globalVar); // Output: Global
``` 
- **Re-declaration Possible**:
```js
var a = 5;
var a = 10;
console.log(a); // Output: 10
```
- **Hoisting**: Variables declared with var are hoisted to the top of their scope, meaning the declaration part is moved to the top, but not the initialization. This can result in undefined behavior if not understood properly.
```js
console.log(hoistedVar); // Output: undefined
var hoistedVar = "Hoisted!";
```
- **Not safe for loop**:
```js
for(var i=0;i<=4;i++)
{
    setTimeout(()=>{
        console.log(i) // 4 4 4 4 4
    },1000)
}
```
- **Not Safe for Closure**:
```js
const funcs = [];
for (var i = 0; i < 3; i++) {
    funcs.push(() => console.log(i)); // make array of functions
}
funcs[0](); // prints 3
funcs[1](); // prints 3
funcs[2](); // prints 3
```
---
## Const:
- **Block Scope**:
- **Re-assignment Error**
- **Must be initilized**
- **No re-declearations**
- **Safe for functions**:
```js
const greet = () => console.log("Hello, world!");
greet(); 

greet = () => console.log("Hi!");
```
- **Immutable Binding, Not Value**: const makes the variable binding immutable, but if the value is an object or array, you can still modify its properties or contents.
```js
const obj = { name: "Pranjal" };
obj.name = "Nanda";
console.log(obj.name); 

const arr = [1, 2, 3];
arr.push(4); 
console.log(arr);
```
```js
const y = 20;
y = 30; // TypeError: Assignment to constant variable.
```
---
## Loops:
- **for , while, do-while, for-in(obj), for-of(Iterable- array,string,set...)**
***
# Functions:
- **Regular Functions**
```js
// Defining a regular function
function greet(name) {
    console.log('Hello, ' + name + '!');
}

// Calling the function
greet('Geek');
```
- Args
```js
function showArgs() {
    console.log(arguments); //{"0":1,"1":2,"2":3}
}
showArgs(1, 2, 3);
```
- Hoisting
```js
greet(); // Output: Hello Geeks!

function greet() {
    console.log('Hello Geeks!');
}
```
- this Keyword
```js
const obj = {
    name: 'Geeks',
    greet: function() {
        console.log(this.name);
    }
};
obj.greet();
```
- **Duplicate parameter names allowed**: it consider he latest val from left to right
---
- **Arrow Functions**
```js
// Defining an arrow function
const greet = (name) => {
    console.log(`Hello, ${name}!`);
};

// Calling the function
greet('Geeks');
```
- Args
```js
const showArgs = (...args) => {
    console.log(args);
};
showArgs(1, 2, 3);
```
- hoisting
```js
greet(); // ReferenceError: Cannot access 'greet' before initialization

const greet = () => {
    console.log('Hello!');
};
```
- this Key word
```js
const obj = {
    name: 'Geeks',
    greet: () => {
        console.log(this.name);
    }
};
obj.greet(); // Output: undefined (inherited from outer scope)
```
- **duplicate parameter name not allowed**
---
- **Immidiatiily Invlocked function**
```js
(function() {
	// IIFE code block
	var localVar = 'This is a local variable';
	console.log(localVar); // Output: This is a local variable
})();
```
# This keyword
- ## Normal Functions:
    - ### Dynamically bound (depends on how it's called)
- ## Arrow Functions:
    - ### Lexically bound (inherits from parent)



## 🔹 1. Object Method Definition

### ❌ Problem with Arrow Function
```js
const user = {
  name: 'Ankan',
  greet: () => {
    console.log(`Hello, ${this.name}`); // ❌ undefined
  }
};
user.greet();
```
**Why?** Arrow functions do not have their own `this`. Here, `this` refers to the global object, not `user`.

### ✅ Correct with Normal Function
```js
const user = {
  name: 'Ankan',
  greet() {
    console.log(`Hello, ${this.name}`); // ✅ Hello, Ankan
  }
};
user.greet();
```

## 🔹 2. Inside setTimeout or setInterval

### ❌ Problem with Normal Function
```js
function Timer() {
  this.count = 0;
  setTimeout(function () {
    this.count++; // ❌ 'this' refers to global object or undefined in strict mode
    console.log(this.count);
  }, 1000);
}
new Timer();
```

### ✅ Fixed with Arrow Function
```js
function Timer() {
  this.count = 0;
  setTimeout(() => {
    this.count++; // ✅ 'this' refers to Timer instance
    console.log(this.count);
  }, 1000);
}
new Timer();
```

## 🔹 3. Using this in Callbacks (e.g., Array methods)

### ❌ Problem with Arrow in Method
```js
const obj = {
  numbers: [1, 2, 3],
  multiplier: 2,
  multiply: () => {
    return this.numbers.map(n => n * this.multiplier); // ❌ this is undefined
  }
};
console.log(obj.multiply());
```

### ✅ Fixed with Normal Function
```js
const obj = {
  numbers: [1, 2, 3],
  multiplier: 2,
  multiply() {
    return this.numbers.map(n => n * this.multiplier); // ✅ Works as expected
  }
};
console.log(obj.multiply());
```

## 🔹 4. Event Handlers in DOM

### ❌ Arrow Function Loses DOM Context
```js
document.querySelector('button').addEventListener('click', () => {
  console.log(this); // ❌ 'this' is not the button element
});
```

### ✅ Use Normal Function to Access DOM Element
```js
document.querySelector('button').addEventListener('click', function () {
  console.log(this); // ✅ 'this' is the button element
});
```

## 🔹 5. Class Methods (React or Vanilla JS)

### ✅ Arrow Function Used to Preserve this Without Binding
```js
class Counter {
  count = 0;

  increment = () => {
    this.count++;
    console.log(this.count); // ✅ Works, no need to bind
  }
}
```

### ❌ Normal Function Requires Binding
```js
class Counter {
  constructor() {
    this.count = 0;
    this.increment = this.increment.bind(this); // ✅ Required to bind
  }

  increment() {
    this.count++;
    console.log(this.count);
  }
}
```

## 🔹 Summary Table

| Scenario                       | Use Arrow Function | Use Normal Function |
|-------------------------------|--------------------|---------------------|
| Callback preserving `this`    | ✅ Yes             | ❌ Needs bind       |
| Object methods needing `this` | ❌ No              | ✅ Yes              |
| Event handler (DOM)           | ❌ No              | ✅ Yes              |
| React class method (arrow)    | ✅ No bind needed  | ❌ Needs binding    |
| Constructor                   | ❌ Not supported   | ✅ Yes              |

## Polyfill :
**In JavaScript, a polyfill is a code implementation that provides modern functionality in older environments where it might not be available. Essentially, it fills the gap for missing features by mimicking how they work in newer JavaScript versions.**

- ### Bind()
```js
let nameObj = {
    name: "Tony"
}

let PrintName = {
    name: "steve",
    sayHi: function () {

        // Here "this" points to nameObj
        console.log(this.name); 
    }
}

let HiFun = PrintName.sayHi.bind(nameObj);
HiFun();
```
- ### Call()
```js
let nameObj = {
    name: "Tony"
}

let PrintName = {
    name: "steve",
    sayHi: function (age) {
        console.log(this.name + " age is " + age);
    }
}

PrintName.sayHi.call(nameObj, 42);
```
- ### Apply()
```js
let nameObj = {
    name: "Tony"
}

let PrintName = {
    name: "steve",
    sayHi: function (...age) {
        console.log(this.name + " age is " + age);
    }
}
PrintName.sayHi.apply(nameObj, [42]);
```
---
## Higher Order Function:
A higher-order function is a function that does one of the following:
- Takes another function as an argument.
- Returns another function as its result.
```js
function fun() {
    console.log("Hello, World!");
}
function fun2(action) {
    action();
    action();
}

fun2(fun);
```
## Closure:
Closures in JavaScript are a feature that allows a function to access variables from its outer scope, even after the outer function has finished executing.

- 2. **Maintaining State in Asynchronous Callbacks**
Closures are often used in asynchronous functions like setTimeout, setInterval, or Promises to capture values properly.
```js
for (var i = 0; i < 3; i++) {
  (function (j) {
    setTimeout(() => console.log(j), 1000);
  })(i);
}
// Output after 1s: 0 1 2 (Correctly captured with closure)
Without closure, using var would log 3 three times.
```

- 3. **Memoization / Caching with Closures**
Closures help implement memoization — storing results of expensive function calls.
```js
function memoizedAdd() {
  let cache = {};

  return function (n) {
    if (n in cache) return cache[n];
    console.log("Calculating...");
    cache[n] = n + 10;
    return cache[n];
  };
}

const add = memoizedAdd();
console.log(add(5)); // Calculating... 15
console.log(add(5)); // 15 (from cache)
```
- 4. **Event Handlers in Loops (Capturing Loop Variables)**
When assigning event handlers in a loop, you often need a closure to capture the current index.
```js
for (let i = 0; i < 3; i++) {
  document.getElementById("btn" + i).addEventListener("click", function () {
    console.log("Button", i, "clicked");
  });
}
```
- If you used var, a closure would be necessary to preserve the i
---
## Curring:
Currying is a functional programming technique where a function with multiple arguments is transformed into a sequence of functions, each taking a single argument.
```js
function hasPermission(role) {
  return function (action) {
    if (role === "admin") {
      return `Allowed to ${action}`;
    } else {
      return `Not allowed to ${action}`;
    }
  };
}

const adminActions = hasPermission("admin");
const userActions = hasPermission("user");

console.log(adminActions("delete user")); // Allowed
console.log(userActions("delete user")); // Not allowed
```
## Event Loop:
- **Call Stack:** JavaScript has a call stack where function execution is managed in a Last-In, First-Out (LIFO) order.
- **Web APIs (or Background Tasks):** These include setTimeout, setInterval, fetch, DOM events, and other non-blocking operations.
- **Callback Queue (Task Queue):** When an asynchronous operation is completed, its callback is pushed into the task queue.
- **Microtask Queue:** Promises and other microtasks go into the microtask queue, which is processed before the task queue.
- **Event Loop:** It continuously checks the call stack and, if empty, moves tasks from the Microtask queue to the stack for execution.After empty the microtask queue it goes to callback queue.
```js
 Promise.resolve()
 .then(() => console.log(1));

 setTimeout(() => console.log(2), 10);

 queueMicrotask(() => {
 console.log(3)
 queueMicrotask(() => console.log(4)) 9});

 console.log(5);
 // 5 1 3 4 2
```
## Promise & Async-await:
| Feature                              | Promise                                                                 | Async/Await                                                        |
|--------------------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------------|
| Definition                           | A Promise represents an intermediate state of an operation and is guaranteed to complete its execution at some point in the future. | Async/Await is syntactic sugar for Promises, making asynchronous code behave more synchronously. |
| States                               | Has 3 states – **pending**, **fulfilled (resolved)**, and **rejected**. | Doesn't have its own states; it works on Promises internally. Returns a Promise that resolves or rejects. |
| Syntax Style                         | Uses `.then()` and `.catch()` chaining.                                | Uses `async` function and `await` keyword inside with `try...catch`. |
| Error Handling                       | Done using `.catch()` method after `.then()`.                          | Done using `try...catch` block.                                     |
| Readability                          | Can become complex and nested (callback hell-like).                    | Cleaner and more readable, especially for sequential tasks.         |
| Parallel Execution Support           | Supports `Promise.all`, `Promise.race`, etc.                           | Also supports `Promise.all`, `Promise.race` with `await`.           |
| Use Case                             | Good for simple or parallel async operations.                         | Best for sequential logic and step-by-step async workflows.         |

```js
const promise = new Promise(function (resolve, reject) {
    const string1 = "geeksforgeeks";
    const string2 = "geeksforgeeks";
    if (string1 === string2) {
        resolve();
    } else {
        reject();
    }
});

promise
    .then(function () {
        console.log("Promise resolved successfully");
    })
    .catch(function () {
        console.log("Promise is rejected");
    });
    // or
    async function demoPromise() {
    try {
        let message = await helperPromise();
        console.log(message);
    } catch (error) {
        console.log("Error: " + error);
    }
}

demoPromise();
```
## Event Delegation:
Event Delegation is basically a pattern to handle events efficiently. Instead of adding an event listener to each and every similar element, we can add an event listener to a parent element and call an event on a particular target using the .target property of the event object.

```js
const customUI = document.createElement('ul');
for (var i = 1; i <= 10; i++) {
const newElement = document.createElement('li');
newElement.textContent = "This is line " + i;
}
newElement.addEventListener('click', () => {
console.log('Responding')
})
customUI.appendChild(newElement);
//==> rather than this we can use 

const customUI = document.createElement('ul');
function responding() {
console.log('Responding')
}
for (var i = 1; i <= 10; i++) {
const newElement = document.createElement('li');
newElement.textContent = "This is line" + i;

}
customUI.appendChild(newElement);
customUI.addEventListener('click', responding)
```
## Event Bubling & Capturing
| Feature                 | Event Bubbling                                        | Event Capturing                                      |
|-------------------------|--------------------------------------------------------|------------------------------------------------------|
| Order of Event Flow     | From **innermost (target)** element to **outermost**   | From **outermost (document)** to **innermost**       |
| Default Behavior        | ✅ Yes, bubbling is default in JavaScript              | ❌ No, capturing is not default                       |
| Propagation Direction   | Child → Parent → Ancestors                            | Parent → Child → Target                              |
| Use Case                | Most common use in event delegation                    | Rarely used, mostly for advanced scenarios            |
| Implementation          | Add event listener normally (`addEventListener`)       | Use `addEventListener` with `capture: true`           |
| Can be stopped by       | `event.stopPropagation()`                             | `event.stopPropagation()`                            |
### Bubling:
```js
<div id="parent">
  <button id="child">Click Me</button>
</div>

<script>
  document.getElementById('parent').addEventListener('click', () => {
    console.log('Parent clicked (bubbling)');
  });

  document.getElementById('child').addEventListener('click', () => {
    console.log('Child clicked');
  });
</script>
/*
Child clicked
Parent clicked (bubbling)
*/
```
### Capturing:
```js
<div id="parent">
  <button id="child">Click Me</button>
</div>

<script>
  document.getElementById('parent').addEventListener('click', () => {
    console.log('Parent clicked (capturing)');
  }, true); // 👈 `true` enables capturing

  document.getElementById('child').addEventListener('click', () => {
    console.log('Child clicked');
  });
</script>
/*
Parent clicked (capturing)
Child clicked
*/
```
## Dobuncing:
In JavaScript, debouncing is a technique used to ensure that a function is not called too frequently. It is commonly used in scenarios where events are triggered rapidly, such as typing in an input field or resizing a window. Without debouncing, functions might be executed many times in quick succession, causing performance issues or unwanted behaviour.
```js
// Debounce function
function debounce(func, delay) {
    let timeout;
    return function (...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// Function to be debounced
function search(query) {
    console.log('Searching for:', query);
}

// Create a debounced version of the search function
const dSearch = debounce(search, 100);

// Simulate typing with multiple calls to the debounced function
dSearch('Hello');
dSearch('Hello, ');
dSearch('Hello, World!');  // Only this call will trigger after 100ms
```
## JSON.parse(), response.json(), JSON.stringify()
| Feature               | `.json()`                          | `JSON.parse()`                                     | `JSON.stringify()`                                     |
|-----------------------|-------------------------------------|----------------------------------------------------|--------------------------------------------------------|
| Belongs To            | `Response` object from Fetch API    | Global JavaScript object                           | Global JavaScript object                               |
| Purpose               | Parses response body to JS object   | Converts JSON string to JS object                  | Converts JS object to JSON string                      |
| Input                 | None (uses response stream)         | A JSON-formatted string                            | A JavaScript object or array                           |
| Output                | A **Promise** that resolves to an object | A **JS object** (synchronously)                    | A **JSON string**                                      |
| Use Case              | When handling HTTP response from `fetch()` | When you have a stringified JSON to work with      | When you want to send/store a JS object as a JSON string |
| Example               | `await res.json()`                  | `JSON.parse('{"name":"Ankan"}')`                   | `JSON.stringify({name:"Ankan"})`                       |
```js
// Using JSON.stringify()
const obj = { name: "Ankan", age: 22 };
const jsonString = JSON.stringify(obj); // Converts JS object to JSON string
console.log(jsonString); // Output: '{"name":"Ankan","age":22}'
//---------------------
// Using JSON.parse()
const jsonString = '{"name": "Ankan"}';
const parsed = JSON.parse(jsonString); // Converts string to JS object
//======================
// Using fetch().json()
const res = await fetch('/api/user');
const data = await res.json(); // Parses response body to JS object
```
## nullish coalescing
The nullish coalescing (??) operator is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.
```js
const data=JSON.parse(localstorage.getItem("user")) ?? [];
```

---
## Scope in JavaScript
- **Global Scope**: Variables declared outside any function or block are in the global scope and accessible anywhere.
- **Function Scope**: Variables declared inside a function are accessible only within that function.
- **Block Scope**: Variables declared with `let` or `const` inside `{}` are accessible only within that block.

```js
let globalVar = "I am global";

function testScope() {
  let functionVar = "I am in function";
  if (true) {
    let blockVar = "I am in block";
    console.log(blockVar); // Accessible here
  }
  // console.log(blockVar); // Error: blockVar not defined
  console.log(functionVar); // Accessible here
}

console.log(globalVar); // Accessible anywhere
testScope();
```

---
## Callback Functions
A callback function is a function passed into another function as an argument, which is then invoked inside the outer function.

```js
function greet(name, callback) {
  console.log('Hello ' + name);
  callback();
}

function callMe() {
  console.log('I am callback function');
}

greet('Ankan', callMe);
```

---
## Prototype & Prototypal Inheritance
Every JavaScript object has a prototype. Objects inherit properties and methods from their prototype.

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log('Hello ' + this.name);
};

const person1 = new Person('Ankan');
person1.greet(); // Hello Ankan
```

---
## Shallow vs Deep Copy
- **Shallow Copy** copies object properties but nested objects are referenced.
- **Deep Copy** copies all nested objects recursively.

```js
const obj1 = { a: 1, b: { c: 2 } };
const shallowCopy = Object.assign({}, obj1);
const deepCopy = JSON.parse(JSON.stringify(obj1));

shallowCopy.b.c = 3;
console.log(obj1.b.c); // 3 (affected by shallow copy)

deepCopy.b.c = 4;
console.log(obj1.b.c); // 3 (not affected by deep copy)
```

---
## Memory Management (Garbage Collection)
JavaScript automatically frees memory by removing objects that are no longer referenced.

---
## ES6+ Features
- **Destructuring**

```js
const person = { name: 'Ankan', age: 22 };
const { name, age } = person;
console.log(name, age);
```

- **Spread Operator**

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4];
console.log(arr2);
```

- **Rest Operator**

```js
function sum(...args) {
  return args.reduce((a, b) => a + b, 0);
}
console.log(sum(1, 2, 3));
```

- **Optional Chaining**

```js
const user = {};
console.log(user?.address?.street); // undefined, no error
```

---
## Modules (import/export)
- Exporting:

```js
// file: math.js
export function add(a, b) {
  return a + b;
}
```

- Importing:

```js
// file: app.js
import { add } from './math.js';
console.log(add(2, 3));
```

---
## Strict Mode ('use strict')
Enables stricter parsing and error handling in JavaScript.

```js
'use strict';
x = 3.14; // Error: x is not defined
```

---
## Data Types & Type Coercion
- JavaScript has dynamic types.
- Type coercion converts values between types automatically.

```js
console.log('5' - 1); // 4 (string to number)
console.log('5' + 1); // '51' (number to string)
```

- Falsy values: `false`, `0`, `''`, `null`, `undefined`, `NaN`

---
## Symbol
A unique and immutable primitive value.

```js
const sym1 = Symbol('desc');
const sym2 = Symbol('desc');
console.log(sym1 === sym2); // false
```

---
## Set and Map
- **Set**: Collection of unique values.

```js
const set = new Set([1, 2, 2, 3]);
console.log(set); // Set {1, 2, 3}
```

- **Map**: Collection of key-value pairs.

```js
const map = new Map();
map.set('a', 1);
console.log(map.get('a')); // 1
```

---
## Object.freeze() and Object.seal()
- `Object.freeze()` makes an object immutable.
- `Object.seal()` prevents adding or removing properties but allows modification.

```js
const obj = { name: 'Ankan' };
Object.freeze(obj);
obj.name = 'Nanda'; // No effect
console.log(obj.name); // Ankan
```

---
## Miscellaneous
- **Service Workers**: Background scripts for offline support.
- **Generator Functions**: Functions that can pause and resume.

```js
function* gen() {
  yield 1;
  yield 2;
}
const g = gen();
console.log(g.next().value); // 1
```

- **eval()**: Executes a string as code (use with caution).
- **with statement**: Extends scope chain (deprecated).
console.log(g.next().value); // 1
console.log('5' + 1); // '51' (number to string)
---  
## Throttling
Throttling ensures a function is only called at most once in a specified period, even if triggered multiple times.

```js
function throttle(func, limit) {
  let inThrottle;
  return function (...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// Usage
const log = () => console.log('Throttled!');
const throttledLog = throttle(log, 1000);
window.addEventListener('resize', throttledLog);
```

---  
## Recursion
A function that calls itself to solve a problem.

```js
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
console.log(factorial(5)); // 120
```

---  
## Pure Function
A function that, given the same input, always returns the same output and has no side effects.

```js
function add(a, b) {
  return a + b;
}
```

---  
## Flattening an Array
Flatten a nested array without using `flat()`.

```js
function flatten(arr) {
  return arr.reduce((acc, val) =>
    Array.isArray(val) ? acc.concat(flatten(val)) : acc.concat(val), []);
}
console.log(flatten([1, [2, [3, 4]], 5])); // [1,2,3,4,5]
```

---  
## Custom Implementation of Array.prototype.map
```js
Array.prototype.myMap = function(callback) {
  let result = [];
  for(let i = 0; i < this.length; i++) {
    result.push(callback(this[i], i, this));
  }
  return result;
};
// Usage
console.log([1,2,3].myMap(x => x * 2)); // [2,4,6]
```

---  
## Custom Implementation of Promise.all
```js
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    let results = [];
    let completed = 0;
    promises.forEach((p, i) => {
      Promise.resolve(p).then(val => {
        results[i] = val;
        completed++;
        if (completed === promises.length) resolve(results);
      }).catch(reject);
    });
  });
}
```

---  
## Polyfill for Object.create()
```js
function create(proto) {
  function F() {}
  F.prototype = proto;
  return new F();
}
```

---  
## Memoization Function
```js
function memoize(fn) {
  const cache = {};
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache[key]) return cache[key];
    const result = fn.apply(this, args);
    cache[key] = result;
    return result;
  };
}
// Usage
const fib = memoize(function(n) {
  if (n < 2) return n;
  return fib(n-1) + fib(n-2);
});
```

---  
## Output-based Quirks

```js
console.log([] + {}); // "[object Object]"
console.log({} + []); // 0 (interpreted as block + array)
console.log(typeof function(){}); // "function"
console.log(typeof null); // "object"
```

---  
## Tagged Template Literals
```js
function tag(strings, ...values) {
  return strings[0] + values.map((v, i) => v + strings[i+1]).join('');
}
const name = "Ankan";
console.log(tag`Hello, ${name}!`); // "Hello, Ankan!"
```

---  
## Tree Shaking
Tree shaking is a technique used in modern bundlers (like Webpack) to remove unused code from final bundles, reducing file size.

---  
## Dynamic Import
```js
// Dynamically import a module
import('./math.js').then(module => {
  console.log(module.add(2, 3));
});
```

---  
## Mixin
A mixin is an object containing methods that can be shared across classes.

```js
const sayHi = {
  hi() { console.log('Hi!'); }
};
class User {}
Object.assign(User.prototype, sayHi);
const u = new User();
u.hi(); // Hi!
```

---  
## Difference: Object.assign() vs Spread Operator
- `Object.assign()` copies properties from source to target object.
- Spread operator (`...`) creates a shallow copy and can merge objects.

```js
const a = {x:1}, b = {y:2};
const c = Object.assign({}, a, b); // {x:1, y:2}
const d = {...a, ...b}; // {x:1, y:2}
```

---  
## Default Function Parameters
```js
function greet(name = "Guest") {
  console.log("Hello, " + name);
}
greet(); // Hello, Guest
```

---  
## How new Keyword Works
- Creates a new object.
- Sets the prototype.
- Binds `this` to the new object.
- Returns the object.

```js
function Person(name) {
  this.name = name;
}
const p = new Person('Ankan');
```

---  
## Static vs Instance Methods
```js
class MyClass {
  static staticMethod() { return 'static'; }
  instanceMethod() { return 'instance'; }
}
console.log(MyClass.staticMethod()); // 'static'
console.log(new MyClass().instanceMethod()); // 'instance'
```

---  
## PreventDefault vs StopPropagation
- `preventDefault()`: Prevents default browser action.
- `stopPropagation()`: Stops event from bubbling up.

```js
element.addEventListener('click', function(e) {
  e.preventDefault();
  e.stopPropagation();
});
```