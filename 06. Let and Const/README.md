# Let and Const

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
