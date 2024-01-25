# Shortest JS Program

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
