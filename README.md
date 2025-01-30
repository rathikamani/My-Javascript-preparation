

Primitives
==============

1 How does hoisting work in JavaScript?
### **Understanding Hoisting in JavaScript**

**Hoisting** is a behavior in JavaScript where variable, function, or class declarations are moved to the top of their scope (global or function) during the **compile phase** before the code is executed. This allows you to reference variables and functions before they are declared in the code.

However, **only declarations are hoisted**, not initializations. Let’s break it down with examples.

---

### **How Hoisting Works**

1. **Variable Hoisting**
   - For `var`, the variable is hoisted and initialized as `undefined`.
   - For `let` and `const`, the declaration is hoisted, but they are not initialized until the code execution reaches their line (this is called the **Temporal Dead Zone**).

2. **Function Hoisting**
   - Function declarations are fully hoisted, meaning you can call them before they are defined.
   - Function expressions (e.g., with `var`, `let`, or `const`) are treated like variables and only hoist the declaration, not the initialization.

3. **Class Hoisting**
   - Classes are hoisted but are not initialized, resulting in a `ReferenceError` if accessed before their declaration.

---

### **Examples**

#### **Hoisting with `var`**

```javascript
console.log(x); // undefined (declaration is hoisted, but initialization is not)
var x = 10;
console.log(x); // 10
```

Here’s how JavaScript interprets the code:

```javascript
var x; // Declaration is hoisted
console.log(x); // undefined
x = 10; // Initialization happens here
console.log(x); // 10
```

---

#### **Hoisting with `let` and `const`**

```javascript
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 20;

console.log(z); // ReferenceError: Cannot access 'z' before initialization
const z = 30;
```

Both `let` and `const` are hoisted, but they remain in the **Temporal Dead Zone** (TDZ) from the start of the block until the declaration is executed.

---

#### **Function Hoisting**

```javascript
foo(); // Works! Outputs: "Hello, world!"
function foo() {
  console.log("Hello, world!");
}
```

But for **function expressions**, only the variable is hoisted:

```javascript
bar(); // TypeError: bar is not a function
var bar = function () {
  console.log("Hello, again!");
};
```

Internally:

```javascript
var bar; // Declaration hoisted
bar(); // Error: bar is undefined at this point
bar = function () {
  console.log("Hello, again!");
};
```

---

#### **Class Hoisting**

```javascript
const obj = new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization
class MyClass {
  constructor() {
    this.name = "Test";
  }
}
```

Classes are hoisted but not initialized, similar to `let` and `const`.

---

### **Key Takeaways**

1. **`var`**:
   - Declaration is hoisted, and initialized as `undefined`.
   - Avoid using `var` in modern JavaScript.

2. **`let` and `const`**:
   - Declaration is hoisted, but they are in the **Temporal Dead Zone** until the code execution reaches them.

3. **Functions**:
   - Function declarations are hoisted completely.
   - Function expressions and arrow functions behave like variables.

4. **Classes**:
   - Hoisted, but not initialized.

---

### **Visualizing Hoisting**

Here’s an example to summarize:

```javascript
console.log(a); // undefined
// console.log(b); // ReferenceError: Cannot access 'b' before initialization
// console.log(c); // ReferenceError: Cannot access 'c' before initialization

var a = 5;
let b = 10;
const c = 15;

function greet() {
  console.log("Hi!");
}

greet(); // Hi!

https://www.youtube.com/watch?v=06093vaHgtg
```
2 Describe the concept of closures.
A closure in JavaScript is a fundamental concept where a function retains access to its lexical scope, even when the function is executed outside that scope. This means that a closure gives you access to an outer function's scope from an inner function.

How Closures Work
When a function is defined, it captures its surrounding lexical environment (the variables and functions in scope at the time of its creation). When this function is returned and executed elsewhere, it still has access to that lexical environment.

Example of a Closure
Here's a simple example to illustrate closures:

function outsideFunction(outerVar) {
  const outerVariable = outerVar

  const localState = 'I will be visible only in this block'

  const insideFunction = (innerVar) => {
    console.log('Outer variable', outerVariable)

    console.log('Inner variable', innerVar)

    console.log('Outer variable (local)', localState)
  }

  return insideFunction
}

const myClosure = outsideFunction('outside')

myClosure('inner')

In this example, insideFunction forms a closure. It captures the variable outerVariable from its outer scope (outsideFunction). When myClosure is called, it still has access to outerVariable, even though outerFunction has finished executing.

3.Explain the event loop and Callback Queue and Call Stack?
What is the Event Loop in JavaScript?
The event loop in JavaScript is a mechanism that allows the programming language to handle multiple tasks (like user interactions, HTTP requests, and timers) without blocking the main thread, even though JavaScript is single-threaded.
It ensures that tasks are executed in the correct order by managing synchronous and asynchronous operations effectively.
________________________________________
How Does It Work?
To understand the event loop, let's break it down into the main components:
1. Call Stack
•	This is where JavaScript executes functions.
•	It can only handle one function at a time (JavaScript is single-threaded).
•	Functions are pushed onto the stack when called and popped off when completed.
2. Web APIs / Background Tasks
•	These are provided by the browser (or Node.js) to handle tasks like: 
o	Timers (setTimeout, setInterval)
o	HTTP requests (fetch, XMLHttpRequest)
o	Event listeners (e.g., click, scroll).
•	They allow JavaScript to delegate time-consuming operations to the browser, so the main thread isn't blocked.
3. Task Queue (or Callback Queue)
•	Once a background task (e.g., a timer or HTTP request) is completed, its callback function is placed in the task queue.
•	The event loop will move these tasks to the call stack when the stack is empty.
4. Event Loop
•	The event loop continuously checks: 
o	Is the call stack empty?
o	If yes, it takes the first task from the task queue and moves it to the call stack for execution.
________________________________________
Step-by-Step Process
Let’s walk through an example:
console.log("1. Start");  // Synchronous

setTimeout(() => {
  console.log("3. Timeout callback"); // Asynchronous
}, 2000);

console.log("2. End");  // Synchronous
What Happens:
1.	console.log("1. Start") is executed → Added to the call stack → Logs "1. Start".
2.	setTimeout is called → It's sent to the Web API to wait for 2 seconds.
3.	console.log("2. End") is executed → Logs "2. End".
4.	After 2 seconds, the callback from setTimeout is placed in the task queue.
5.	The event loop checks the call stack (it's now empty) and moves the callback to the stack → Logs "3. Timeout callback".
Output:
1. Start
2. End
3. Timeout callback
________________________________________
Key Concepts
1.	Synchronous vs Asynchronous Tasks
o	Synchronous: Executed immediately in the call stack (e.g., console.log).
o	Asynchronous: Delegated to Web APIs and executed later via the event loop (e.g., setTimeout, fetch).
2.	Non-Blocking
o	The event loop allows JavaScript to perform heavy operations like fetching data or waiting for user input without blocking the main thread.
3.	Order of Execution
o	Synchronous code runs first.
o	Then, asynchronous callbacks are processed in the order they are added to the task queue.
________________________________________
Example with Promises (Microtask Queue)
JavaScript also has a microtask queue for tasks like Promise.then and MutationObserver. Microtasks have a higher priority than regular tasks.
console.log("1. Start");

setTimeout(() => {
  console.log("3. Timeout callback");
}, 0);

Promise.resolve().then(() => {
  console.log("2. Promise resolved");
});

console.log("4. End");
Output:
1. Start
4. End
2. Promise resolved
3. Timeout callback
Why?
1.	Promise.then goes to the microtask queue, which is handled before the task queue.
2.	The event loop processes the microtasks (Promise) first, then tasks (setTimeout).
________________________________________
Visualizing the Event Loop
1.	Call Stack: Executes synchronous tasks.
2.	Web APIs: Handles async tasks.
3.	Task Queue: Stores callbacks for async tasks.
4.	Microtask Queue: Stores high-priority async tasks (like Promises).
5.	Event Loop: Moves tasks from the queues to the stack when it’s empty.
________________________________________
Summary
•	The event loop is the system that ensures JavaScript executes tasks in the right order.
•	It allows JavaScript to handle asynchronous operations in a non-blocking way.
•	The flow is: Call Stack → Web APIs → Task Queue/Microtask Queue → Event Loop.
Let me know if you want a diagram or further clarification! 😊

4.What is the difference between == and ===?
5.How do you check the type of a variable in JavaScript?
6.What is the use of the this keyword in JavaScript?
7.High-Order functions?
8.call apply bind?
9.Currying?
Currying in JavaScript is a technique the transforms a function with multiple arguments into a 
Sequence of functions, each taking a single argument.
Example:
Const sum = function(a){
      Return function(b) {
Return a+b;
}
}
Const answer = sum(5)(6)
Output: 11

Arrow function:
Const sum = a=> b=> a+b;

Q:2
Evaluate(‘add’)(4)(2) => 6
Evaluate(‘sub’)(4)(2) => 6

Evaluate(‘mul’)(4)(2) => 6

Evaluate(‘div’)(4)(2) => 6



10.Event bubbling and capturing?
When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on the other ancestors.
Event capturing is opposite to the event bubbling, in the event capturing the flow goes from outermost element to the target element.
Ex:
Event bubbling:
<div class=”Parents”>
Parent
<div class=”child”>
Child
</div>
</div>
document.queryselector(‘.parents’).addEventListener(‘click’,()=>{
console.log(‘parent’);
});
document.queryselector(‘.child’).addeventListener(‘click’,()>{
console.log(‘child’);
});

Output:
 

Event capturing:
 
11.Event delegation?
12.Debouncing and throttling?
Debouncing and throttling are techniques used to control the rate at which a function is executed, particularly in scenarios where a function is triggered repeatedly in quick succession (e.g., scrolling, resizing, typing).
________________________________________
1. Debouncing
Debouncing ensures that a function is executed only after a specified delay has passed since the last time it was invoked. It’s useful for reducing the frequency of events like typing in a search box or window resizing.
How It Works:
•	When the event is triggered, a timer is set.
•	If the event is triggered again before the timer completes, the timer resets.
•	The function runs only after the timer expires without interruption.
Example: Search Input
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer); // Clear the previous timer
    timer = setTimeout(() => func.apply(this, args), delay); // Set a new timer
  };
}

// Usage
const search = () => {
  console.log('Search query sent:', new Date().toISOString());
};

const debouncedSearch = debounce(search, 500);

document.getElementById('searchInput').addEventListener('input', debouncedSearch);
•	Behavior: The search function executes only when the user stops typing for 500ms.
________________________________________
2. Throttling
Throttling ensures that a function is executed at most once every specified interval, even if the event is triggered multiple times during that interval. It’s useful for scroll or resize events where frequent execution can hurt performance.
How It Works:
•	When the event is triggered, the function executes immediately.
•	Then, it ignores subsequent triggers until the specified interval has passed.
Example: Scroll Event
function throttle(func, interval) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= interval) {
      lastCall = now;
      func.apply(this, args);
    }
  };
}

// Usage
const handleScroll = () => {
  console.log('Scroll event handled:', new Date().toISOString());
};

const throttledScroll = throttle(handleScroll, 1000);

window.addEventListener('scroll', throttledScroll);
•	Behavior: The handleScroll function executes at most once every 1000ms, regardless of how often the scroll event is triggered.
________________________________________
Differences Between Debouncing and Throttling
Feature	Debouncing	Throttling
Execution	Delays execution until the event stops.	Executes periodically during the event.
Use Case	Search boxes, form validation, resizing.	Scrolling, resizing, mouse movement.
Frequency	Executes once after inactivity.	Executes at regular intervals.
________________________________________
Combined Example
Suppose you have a button that triggers an expensive operation like API calls, and you want to both debounce and throttle it.
const handleClick = () => {
  console.log('Button clicked:', new Date().toISOString());
};

// Debounce: Wait 300ms after the last click
const debouncedClick = debounce(handleClick, 300);

// Throttle: Allow click only once every 1000ms
const throttledClick = throttle(debouncedClick, 1000);

document.getElementById('myButton').addEventListener('click', throttledClick);
 

 

13.Pure and Impure Functions?
14.Factory Function?



Function
============

objects
=========


Arrays
=======



Asynchronous
==============
- How async js code works?
- async/defer

Variables
===========
Explain the difference between let, const, and var.
Here’s an explanation of the differences between `let`, `const`, and `var` in JavaScript, summarized in a table with examples.

---

### **Difference Between `let`, `const`, and `var`**

| Feature                       | `var`                        | `let`                        | `const`                      |
|-------------------------------|------------------------------|------------------------------|------------------------------|
| **Scope**                     | Function or global scope     | Block scope                 | Block scope                 |
| **Re-declaration**            | Allowed within the same scope| Not allowed in the same scope| Not allowed in the same scope|
| **Initialization**            | Optional                    | Optional                    | Mandatory (requires a value at declaration) |
| **Reassignment**              | Allowed                     | Allowed                     | Not allowed                 |
| **Hoisting**                  | Hoisted and initialized as `undefined` | Hoisted but not initialized | Hoisted but not initialized |
| **Use Case**                  | Older code, avoid using in modern JavaScript | Variables that may change | Constants or immutable values |

---

### **Examples of Each**

#### **Using `var`**

```javascript
// Function scope
function testVar() {
  var x = 10;
  if (true) {
    var x = 20; // Same variable, redefined
    console.log(x); // 20
  }
  console.log(x); // 20 (not block-scoped)
}

testVar();

// Hoisting
console.log(a); // undefined
var a = 5;
```

---

#### **Using `let`**

```javascript
// Block scope
function testLet() {
  let x = 10;
  if (true) {
    let x = 20; // Different variable due to block scope
    console.log(x); // 20
  }
  console.log(x); // 10 (block-scoped)
}

testLet();

// Hoisting
// console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 5;
```

---

#### **Using `const`**

```javascript
// Block scope
function testConst() {
  const x = 10;
  if (true) {
    const x = 20; // Different variable due to block scope
    console.log(x); // 20
  }
  console.log(x); // 10 (block-scoped)
}

testConst();

// Reassignment
const c = 5;
// c = 10; // TypeError: Assignment to constant variable

// Hoisting
// console.log(d); // ReferenceError: Cannot access 'd' before initialization
const d = 5;
```

---

### Key Points to Remember

- **Use `let`** when a variable’s value needs to change.
- **Use `const`** for values that should not change (constants).
- **Avoid `var`** in modern JavaScript, as it can lead to bugs due to its function/global scope and hoisting behavior.

2)Create Variables with Object and Array and Log Their Types

let user = {
    name: "Alice",
    age: 30
};
let colors = ["red", "green", "blue"];
 
console.log(typeof user); // "object"
console.log(typeof colors); // "object" (arrays are objects)
Notes

Both arrays and objects are identified as "object" type in JavaScript.
