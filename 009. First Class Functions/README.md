# First Class Functions

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

