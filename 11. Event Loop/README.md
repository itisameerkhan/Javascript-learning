# Event Loop

The event loop is a fundamental concept in asynchronous programming, particularly in environments like JavaScript. **It's a mechanism that allows programs to handle multiple tasks concurrently without blocking the execution of code**. The event loop enables non-blocking I/O operations, making it crucial for building responsive and efficient applications.

* **Event Loop**: The event loop is a continuous process that constantly checks the `callback queue` for events or tasks. It runs in the background while the main program executes.

* **Callstack**: The call stack is a data structure that keeps track of the currently executing function or operation. When a function is called, it gets added to the call stack.

* **Callback Queue(Task Queue)**: Asynchronous operations, such as timers, network requests, or user interactions, are handled outside the main program flow. When these asynchronous tasks are completed, their associated callbacks are pushed into the callback queue.

* **Event Loop Iteration:** In each iteration of the event loop, the system checks the callback queue for any pending tasks.

* **Execution of Callbacks:** If there are callbacks in the queue, they are moved to the call stack for execution. The call stack processes these callbacks one by one.

* **Non-Blocking Nature:** Importantly, the event loop ensures that asynchronous tasks don't block the main program's execution. Instead, the callbacks are scheduled to run when the call stack is empty.

![el7](/assets/el8.webp)

### Callback Queue

* The Callback queue is a data structure that operates on the FIFO (first-in-first-out) principle.
* Callback functions that need to be asynchronously executed, are pushed onto the callback queue.
* These are later pushed to the Call stack to be executed (when the event loop finds an empty call stack).

### Web APIs

* setTimeout()
* DOM APIs
* fetch()
* localStorage
* console
* location

```js
console.log("start");

setTimeout(function callback() {
  console.log("callback function")
}, 5000);

console.log("end")
```

output:
```
start
end
callback function
```

* ###  step  1

Global Execution context is created and push it into the callstack and the code gets executed synchronously.

![el1](/assets/el1.png)

#### console
```
start
```

* ### Step 2

 `setTimeout` function register timer in WEB APIs with delay of 5000 milliseconds

 ![dl2](/assets/el2.png)



* ### Step 3 

after reaches line 3 

### console
```
start
end
```

### Step 4 

After complete execution of global execution context, then its pops out of **callstack** but still the timer stills running

![el3](/assets/el3.png);

### Step 5

after timer runs out. `callback` function pops out, then push into callback queue.

![el4](/assets/el4.png)

#### Step 6

 **Event loop** checks for the `callback  queue` it there anything to execute, if its finds function and push it into the `callstack`.

 ![el6](/assets/el6.png)

 **console**

 ```
 start
 end
 callback function
 ```

 ###  Step 7 

 `callback` function pops out of callstack

 ![el8](/assets/el7.png)


 ### Why we need callback Queue ?
 
 **Event Loop** constantly checking whether the `callstack` is empty and when its empty it pushes the task from `callback queue` to `callstack`.

 **Non-Blocking Execution:**  The callback queue allows these operations to be asynchronous, ensuring that they don't block the main thread.

 **Event Loop Coordination:**  The event loop continuously checks the call stack for currently executing code. If the call stack is empty, the event loop looks into the callback queue for pending tasks. This coordination between the event loop and the callback queue ensures that asynchronous operations are executed at the appropriate time.


### MicroTask Queue

When the asynchronous task is performed with the help of javascript `promises`, the output from the web browser is pushed to the microtask queue. When the code contains only `promises` it works the same way as explained in the example of the callback queue. The only difference is that instead of a callback queue, the web browser output is pushed onto the microtask queue upon completion.

**All the callback functions comes from promises are push into mirotask queue.**

#### Then how does the callback queue behaves differently from the microtask queue?

The **Microtask queue has a higher priority than the callback queue** which means that if both queues are scheduled to be executed at the same time, the microtask queue will be executed first. 

**Priority**: Microtasks have higher priority than regular tasks. When the JavaScript engine checks for tasks in the event loop, it processes all available microtasks before moving on to the next regular task.

**Sources of Microtasks:** Common sources of microtasks include promises, mutation observers, and certain APIs like process.nextTick in Node.js. When promises are resolved or certain asynchronous operations occur, corresponding microtasks are added to the microtask queue.

![mt1](/assets/mt1.gif)

 ### How does this works on `fetch()` 

 ```js
 console.log("start");

 setTimeout(function cbT() {
  console.log("CB SetTimeout");
 }, 5000);

 fetch("https://api.netflix.com")
 .then(function cbF() {
  console.log("CB netflix");
 })

 console.log("END");
 ```

  ```
  start
  END
  CB netflix
  CB setTimout
  ```

  ![demo](/assets/mt2.png)
  ---
  ![demo](/assets/mt3.png)
  ---
  ![demo](/assets/mt4.png)
  ---
  ![demo](/assets/mt5.png)
  ---

  ### Difference Between Callback queue and Microtaask Queue

  |sno. | callback queue | microtask queue |
  | --- | --- | ---- |
  | 1. | is a queue that holds tasks scheduled to be executed after the current task completes. |  is a queue specifically designed for handling microtasks.
  | 2. |  Handles general asynchronous tasks and callbacks, often associated with I/O operations, timers, and events. | Specifically designed for microtasks, which are tasks with higher priority than regular tasks. Common sources include promises, mutation observers, and certain APIs.
  ---