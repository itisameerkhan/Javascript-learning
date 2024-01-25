# Closures

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