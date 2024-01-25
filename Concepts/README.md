## Concepts 

| no. | Context |
| --- | ----- |
| 1. | [Execution Context](#execution-context) 
| 2. | [Call stack](#call-stack)
| 3. | [Hoisting](#hoisting)
| 4. | [Shortest JS Program](#shortest-js-program)
| 5. | [undefined Not-Defined null](#undefined-not-defined-null)
| 6. | [let and Const](#let-and-const)
| 7. | [Block Statement](#block-statement)
| 8. | [Closures](#closures)
| 9. | [First Class Functions](#first-class-functions)
| 10.| [Callback Functions](#callback-functions)
| 11.| [Event Loop](#event-loop)

---

### Execution Context
    
Everything happens inside a Execution context

**The browser's javascript engine creates a special environment to handle the transformation and execution of javascript code.**

Execution context has a two component

* **Memory component** - is also knows as variable environment which contains variables and functions as a key-value pairs.

* **Code component** - is also known as a thread of execution where javascript code is executed one line at a time

<img src='https://res.cloudinary.com/practicaldev/image/fetch/s--m75dCi9q--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4gyh6glkq7ofmvrb1low.png' >

**Javascript is synchronous single threaded language**  

* single threaded means that javascript can execute one command at a time

* Synchronous single-threaded means that it can execute one command in order at a time.

#### How is Execution context is created and how is the program run ? 

When JavaScript code runs Global Execution Context (GEC) is created. Execution of code is happening in two phases:

* **Phase 1 (Creation Phase)** is allocating memory to the variables and functions. For all variables value stored in memory is undefined and functions are copied in memory.

* **In Phase 2 (Execution Phase)** JavaScript code is executed line by line and it is defining variables in memory here. Every function invoked creates its own local execution context, which is put in call stack (explained in the next chapter).

### What happens when you run javascript code

```js 
var n = 2;
function square(num) {
    var ans = num * num;
    return ans;
}
var x = square(n);
var y = square(4);
```

#### phase - 1

![demo](/assets/demo2.png)

#### phase - 2

![demo3](/assets/demo3.png)
![demo4](/assets/demo4.png)
![demo5](/assets/demo5.png)

 when you invoke a function, a whole new execution context is created

 [ui dev](https://ui.dev)


### Call Stack

 A call stack is a mechanism for an interpreter (like the JavaScript interpreter in a web browser) to keep track of its place in a script that calls multiple functions — what function is currently being run and what functions are called from within that function, etc.

 JavaScript has its own Call stack. It behaves like a normal stack where we have Global Execution Context stored at a bottom of the stack whenever a JavaScript program is run.

 There are two kinds of Execution Context in JavaScript:

 *  Global Execution Context (GEC)
 * Function Execution Context (FEC)

 keyword `return` returns control of the program back to the place where a function was invoked. Whenever a function is invoked, a new execution context is created on the top of GEC. When a function returns a value, the function execution context is popped out of a stack and the control goes back to the Global Execution Context where it is left.

 Call stack maintains the order of execution of “Execution Contexts” and it is also known as:

 * Execution Context stack
 * Program stack
 * Control stack
 * Runtime stack
 * Machine stack

 [what is execution context in javascript](https://prototyp.digital/blog/what-is-execution-context-in-javascript)

 **Javascript maintains the order of execution of execution context**
 
 ![callstack](/assets/Call-stack.gif)

[🔝Back to Top](#concepts)

---

3. ### Hoisting

 Hoisting is a behavior in JavaScript where variable and function declarations are moved to the top of their containing scope during the compilation phase, before the actual code execution.

In javascript where you can access functions before you initialized them and if you try to access variables before initializing you will get the value of `undefined`.

#### Variable hoisting 
 * Variable declarations using var are hoisted to the top of their containing scope. However, only the declarations are hoisted, not the initializations.
 * This means that you can use a variable before it's declared in the code, but the value will be undefined until the actual declaration is reached.

 ```js 
 console.log(x); // Outputs: undefined
 var x = 5;
 console.log(x); // Outputs: 5
 ```

 **Note**: *Hoisting does not occur with variables declared using let and const until the line where they are declared.*

#### Functional Hoisting 

* Function declarations are hoisted along with their entire definition, including the body of the function.
* This means that you can call a function before it appears in the code.

```js
sayHello(); // Outputs: Hello
function sayHello() {
  console.log('Hello');
}
```

* Function expressions (e.g., assigning a function to a variable) do not exhibit the same hoisting behavior.

```js
// This won't work due to hoisting limitations with function expressions
sayHi(); // Error: sayHi is not a function
var sayHi = function() {
  console.log('Hi');
};
```

[🔝Back to Top](#concepts)

---

4. ### Shortest JS Program

![shortjs](/assets/demo6.png)

 **What happens when empty file run ?**

 It creates a [Global Execution Context](#execution-context) and push it into the [Call Stack](#call-stack). and also creates `window` object. `window` is a global object. along with that `this` variable is also created.

 ```js
 this === window // true
 ```

 `this` is pointed to the `window`

 ![window](/assets/widnwo.png)

 ```js
 var a = 10;
 function b() {
    var c = 10;
 }
 ```
 ![window](/assets/window2.png)

 The global variable attached to the `window` like `a` and function `b` but not the local variable `c`.

 we can get the value through this

```js
console.log(a) // 10 
console.log(window.a); // 10  
console.log(this.a) // 10
```

[🔝Back to Top](#concepts)


5. ### Undefined Not-defined Null

 * `undefined`:  In JavaScript, `undefined` is a primitive value and a type. It indicates that a variable has been declared but has not been assigned a value. Additionally, it can be the default value of function parameters that are not provided.

 ```js
  var x; 
  typeof(x) // undefined
 ```
---
* `not defined`: The term "not defined" is often used when a variable or identifier is used without being declared at all. This results in a ReferenceError.

```js
console.log(x) // ReferenceError: x is not defined
```

```js 
null == undefined // true 
null === undefined // false
```

---

 * `null`: assignment value given to a variable. The variable which has been assigned to `null` has no value.
 * When we assign null as a value to any variable, it means that it is empty or blank. It is to show that the variable has no value.
 * Also, null is an **object** in JavaScript. 

 ```js
 var x = null
 typeof(null) // object
 ```

[🔝Back to Top](#concepts)

 ---

 6. ### Let and Const

  `let`: 
  * `let` declarations are scoped to blocks as well as functions.
  * `let` is **hoisted** in JavaScript, but it behaves differently compared to `var`. When a variable is hoisted with `let`, it is hoisted to the top of its block, but it is not initialized (assigned a value) until the actual declaration statement is encountered in the code. This is known as the **temporal dead zone.**
  * `let` declarations do not create properties on `globalThis` when declared at the top level of a script.
  * `let` declarations cannot be redeclared by any other declaration in the same scope.

  ![demo10](/assets/demo10.png)

  #### Temporal Dead Zone

  The **temporal dead zone (TDZ)** is a specific period in the execution of JavaScript code where variables declared with `let` and `const` exist but cannot be accessed or assigned any value. During this phase, accessing or using the variable will result in a ReferenceError.

  ```js
  console.log(x); // ReferenceError: cannot access 'x' before initialization
  let x = 10;
  ```

  `const`: 

In JavaScript, the `const` keyword is used to declare a constant variable, meaning a variable whose value cannot be reassigned once it has been initialized. Constants are block-scoped, like variables declared with let.

**Immutability**:  Once a value is assigned to a const variable, it cannot be changed or reassigned. Any attempt to reassign a value to a const variable results in a `TypeError`. 

```js
const PI = 3.14;
PI = 3.14159; // TypeError: Assignment to constant variable.
```

```js
const a; // SyntaxError: Missing initializer in const declaration
a = 10;
```
[🔝Back to Top](#concepts)

---

7. ## Block Statement

  In JavaScript, a block statement is a group of statements enclosed in curly braces `{}`. It is used to group multiple statements together into a single compound statement. A block statement can be used wherever a single statement is expected.

 ```js
 {
  // statement 1
  // statement 2
  // ...
  // statement n
}
 ```

 ### Block Scope

 The variables and functions that can be accessed inside block statement. 

 ```js
 {
  var a = 10;
  let b = 20;
  const c = 30;
 }
 console.log(a); // 10
 console.log(b); // Uncaught ReferenceError: Cannot access 'b' from debugger
 console.log(c); // Uncaught ReferenceError: Cannot access 'c' from debugger
 ```

 ![demo](/assets/dem11.png)

 ### Shadowing in JS

 
In JavaScript, shadowing occurs when a variable declared within a certain scope has the same name as a variable in an outer scope. The inner variable **shadows** the outer variable, making the outer variable temporarily inaccessible within the inner scope.

```js
var a = 10;
{
  var a = 100;
}
console.log(a) // 100
```

```js 
let a = 10;
const b = 20;
{
  let a = 100;
  const b = 200;
}
console.log(a) // 10;
console.log(b) // 20
```

### Illegal shadowing 

```js
var a = 10;
{
  let a = 10; ✅
}
```

```js
let a = 10;
{
  var a = 10; ❌ // SyntaxError: Identifier 'a' has already been declared
}
```
```js
let a = 10;
{
  let a = 20; ✅
}
```

### Lexical Scope Chain 

```js
const a =  10;
{
  const a = 10;
  {
    const a = 10;
  }
}
```

![demo](/assets/demo8.png)

[🔝Back to Top](#concepts)

---

8. ## Closures

  A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

  Closure means  *functions* binded together with the lexical environment.

  ```js
  function x() {
    var a = 7;
    function y() {
      console.log(a);
    }
    y();
  }
  x();
  ```

  ![demo](/assets/demo9.png)


  ```js
  function x() {
    var a = 7;
    function y() {
      console.log(a);
    }
    return y;
  }

  var z = x();
  z(); // 7
  ```

  when the function returns its function, it still maintain its **lexically scope and closures** with it.

  ```js
  function z() {
      var b = 900;
      function x() {
          var a = 7;
          function y() {
              console.log(a,b);
          }
          y();
      }
      x();
  }
  z();
  ```

  ![demo](/assets/demo12.png)

  **uses of closures**
  * Module Design Pattern
  * Currying
  * functions like once
  * memoize
  * maintaining state in `async` world
  * setTimeouts
  * Iterators
  * and many more.

   [🔝Back to Top](#concepts)

---

## First Class Functions

  ### Function Statement

  ```js
  function doSomething() {

  }
  ```

  ### Function Expression

  ```js
  const doSomething = function () {

  }
  ```

  *Difference between the function statement and function expression is [hoisting](#hoisting)*


  ### Function Declaration 

  ```js
  function doSomething () {

  }
  ```

  ### Anonymous Function 

  Anonymous function doesn't have identity. Instead of declared with specific identifier. it is defined **inline** where it is needed. **Anonymous functions are often used in the situation where a used as an argument to an another function or assigned to a variable**

  ```js
  (function() {
    console.log('something');
  })();
  ```

### First Class Functions

In Javascript functions are like first-class citizens, which means they can be treated like any other value(such as string, object, numbers). This property of function bring many features to the language.

For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.

1. #### Assigning to a variable

  you can assign a function to a variable

  ```js
  const doSomething = function() {

  }
  ```

2. #### Passing an Argument.

Functions can be passed as an argument to other functions.

```js
function greet(callback) {
  callback();
}

greet(function() {
  console.log('namaste 🙏 javascript');
})
```

3. #### Returing from functions 

Functions can be returned from other functions

```js
function createMultiplier(factor) {
  return function(x) {
    return x * factor;
  }
}

const double = createMultiplier(2);
console.log(double(5)) // output: 10
```

4. #### Storing in Data structures 

functions can be used in objects or arrays.

```js
const functionArray = [
  function fun1() { console.log('function 1'); },
  function fun2() { console.log('function 2'); },
  function fun3() { console.log('function 3'); },
]

functionArray[1](); // function 2
```


[🔝Back to Top](#concepts)

---

10. ## Callback Functions

`callback` functions are the functions that are passed as a argument to another functions and which is then invoked inside the outer function to complete some kind or routine or actions. callback are used to handle asynchronous operations, events, or other scenarios where the timing of an operation is uncertain.

```js
setTimeout(function() {
  console.log('inside callback function');
},5000);
```

This function executed after 5 seconds, moreover also this function pushed into the `callstack` 

![callback](/assets/callback.png)

In this Figure, 
* `(anonymous) script:js:1` for the function `setTimeout`
* `(anonymous) script:js:2` for the **callback function** that passed as a argument.

```js
function eventListenerFunction() {
    let count = 0;
    document.querySelector('button')
    .addEventListener('click', function handleClick() {
        console.log('button clicked -> ', ++count);
    })
}

eventListenerFunction();
```

In this Code, both **Callback and closure** functions play roles.

1. #### Closure

  The `handleClick` function is defined inside the `eventListenerFunction`. This creates a closure, meaning the inner function (`handleClick`) has access to the outer function's variables and parameters, even after the outer function (`eventListenerFunction`) has finished executing. In this case, `handleClick` has access to the `count` variable even though it's declared in the outer function.

2. #### Callback Functions

The `handleClick` function is also a callback function. It is passed as an argument to the `addEventListener` method. This means that when the button is clicked, the `handleClick` function will be called back (invoked) by the event listener. In this callback function, the `count` variable is incremented and logged to the console.

![callback](/assets/callback2.png)

### Garbage Collection & removeEventListeners

1. #### Garbage Collections

  * Garbage collection is the process of automatically detecting and freeing up memory occupied by objects that are no longer reachable or in use by the program.

  * If memory occupied by unused objects is not released, it can lead to memory leaks. Garbage collection helps prevent memory leaks by identifying and releasing memory that is no longer needed.

  * By automatically managing memory, garbage collection reduces the chances of the program running out of memory. It allows developers to focus on writing code rather than manually managing memory, improving productivity.

2. #### removeEventListener

  * Event listeners, when not removed properly, can lead to memory leaks. If an object with an attached event listener is not removed, it stays in memory even if it's no longer needed, preventing garbage collection.

[🔝Back to Top](#concepts)

---

11. ## Event Loop



[🔝Back to Top](#concepts)

---