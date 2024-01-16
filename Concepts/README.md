## Concepts 

| no. | Context |
| --- | ----- |
| 1. | [Execution Context](#execution-context) 
| 2. | [Call stack](#call-stack)
| 3. | [Hoisting](#hoisting)
| 4. | [Shortest JS Program](#shortest-js-program)
| 5. | [undefined Not-Defined null](#undefined-not-defined-null)
| 6. | [let and Const](#let-and-const)


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

---