# Execution Context
    
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


