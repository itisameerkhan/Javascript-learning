# Callback Functions

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
