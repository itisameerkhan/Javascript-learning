 # Hoisting

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
