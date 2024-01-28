# setTimeout ⏰

`setTimeout` is a function in JavaScript used to schedule the execution of a specified function or piece of code after a specified amount of time has elapsed. It allows you to introduce delays in the execution of code.

```js
console.log('start');

setTimeout(() => {
    console.log('timer');
}, 5000)

console.log('end');
```

#### output

```
start
end
timer
```

* **console.log('start'):** This line logs "start" to the console immediately.

* **setTimeout(() => { console.log('timer'); }, 5000);**: The `setTimeout` function is called, scheduling the anonymous callback `function (() => { console.log('timer'); })` to be executed after a delay of 5000 milliseconds (5 seconds). However, this does not block the execution of the next line.

* **console.log('end'):** This line logs "end" to the console immediately.

Even though the `setTimeout` is set for a 5-second delay, it doesn't pause the execution of the program. The callback function will be added to the event queue after the specified delay. The event loop will eventually pick up this callback and execute it when the main execution thread is idle.

--- 

## consider this example

```js
function x() {
    for(var i=1;i<=5;i++) {
        setTimeout(function() {
            console.log(i);
        }, i * 1000);
    }
}

x();
```

### output

```
6
//after 1 second
6
//after 1 second
6
//after 1 second
6
//after 1 second
6
```

This code defines a function x that contains a loop with `setTimeout` calls. The goal might be to log values from 1 to 5 with a delay, increasing by seconds.

However, there's a common JavaScript closure issue with the use of `var` inside the loop. **The `var` keyword does not have block scope, so the variable i is shared among all the iterations.** When the `setTimeout` callbacks are executed, they all reference the same variable i, which, after the loop finishes, will have the final value of 6.

--- 

```js
function x() {
    for(let i=1;i<=5;i++) {
        setTimeout(function() {
            console.log(i);
        }, i * 1000);
    }
}

x();
```

### output

```
1
//after 1 second
2
//after 1 second
3
//after 1 second
4
//after 1 second
5
```

The key difference here is the use of `let` instead of `var` to declare the loop variable `i`. The introduction of `let` creates a new block-scoped variable `i` for each iteration of the loop.

* The loop runs from i = 1 to i = 5.
* For each iteration, a setTimeout is scheduled with a delay based on the value of the block-scoped i (1 second for the first, 2 seconds for the second, and so on).
* Because of block scoping, **each closure created by the setTimeout function captures the correct and distinct value of i for its respective iteration.**

--- 

### How to works with `var` keyword ?

```js
function x() {
  for(var i=1;i<=5;i++) {
      function closure(i) {
          setTimeout(function() {
              console.log(i);
          }, i * 1000);
      }
    closure(i);
  }
}

x();
```

### output

```
1
//after 1 second
2
//after 1 second
3
//after 1 second
4
//after 1 second
5
```

### Here's the breakdown:

* The for loop runs from **i = 1 to i = 5.**
* Inside the loop, the closure function is invoked with the current value of i as an argument.
* The closure function creates a closure, **capturing the current value of i.**
* Within the closure, a `setTimeout` function is used to log the captured value of i after a delay (i * 1000 milliseconds).

---


# Trust Issues with `setTimeout`

```js
function cb() {
    console.log('callback function')
}

setTimeout(cb,5000);
```

`setTimeout` function doesn't invoke callback function after exactly 5000 milliseconds. it depends on the callstack.

#### Consider this example 

```js
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 5000);
const baz = () => console.log("Third");

bar();
foo();
baz();
```

![demo](/assets/demo18.gif)

1. global execution context is created and pushed into callstack.

2. code runs line by line
3. **start** will be printed on the console.
4. `setTimeout` register callback function in WebAPIs and starts timer by 5 seconds.
5. **end** will printed on the console.
6. callstack gets empty.
7. event loop constantly checks for the callstack and callback queue. when the callstack is empty. which pushes the callback function into callstack then started executing it.
8. **callback funtion** will be printed.

> to know more about event loop, [click this](/011.%20Event%20Loop/README.md)

* Suppose if there are million lines of code which takes 10 seconds to run, while on the other hand **callback** function is expired after 5 seconds and pushed into the **callback queue**, it will not immediately pushed into the **callstack** because there are million lines of code which takes 10 seconds to run. 

* Event loop constantly checking whether the callstack is empty, then it pushes the callback function into the callstack.

* After 10 seconds, global execution context will be removed from the callstack, then **callback function** been waiting on the **callback queue** gets the chance to execute on the callstack with the help of **event loop**. also known as concurrency model.

**This is reason for `setTimeout` has trust issues**

```js
console.log('start');

setTimeout(() => {
  console.log('callback');
}, 5000);

console.log("end");

let startDate = new Date().getTime();
let endDate = startDate;

while(endDate < startDate + 10000) {
  endDate = new Date().getTime(); // exactly runs for 10 seconds
}

console.log("while expires");
```

1. **start** will be printed

2. `setTimeout` registers callback function in WebAPIs and pops out of callstack.
3. **end** will be printed.
4. while loop runs for 10 seconds, which will block the main thread for 10 seconds to complete. on the otherhand callback function from the `setTimeout` already expires and waiting in ***callback queue***
5. after 10 seconds **while expires** and **callback** will be printed in the console.

```
start
end
>>> (after 10 seconds ⌛)
while expires
callback
```

This is why `setTimeout` doesn't guaranted it will takes exaclty 5 seconds. but it **atleast** takes 5 seconds.

---

### Another example

```js
console.log('start')

setTimeout(function() {
    console.log('callback');
},0);

console.log('end');
```

```
start
end
callback
```

### Code Explanation

* Even though `setTimeout` timer is 0, it will goes register through WebAPIs, and pushes into the **callback queue**.

* once the **callstack** is empty then **callback** function is gets executed.

#### Why we need to put  `setTimeout` to **zero**

* To Differ the function.
* Updating the UI.