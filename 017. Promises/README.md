# 💫 Promises

![demo](/assets/demo22.png)

The very first thing we need to do, is get the image that we want to edit. A `getImage` function can take care of this! Only once that image has been loaded successfully, we can pass that value to a `resizeImage` function. When the image has been resized successfully, we want to apply a filter to the image in the `applyFilter` function. After the image has been compressed and we've added a filter, we want to save the image and let the user know that everything worked correctly! 🥳

![demo](/assets/demo23.png)

Hmm... Notice anything here? Although it's... fine, it's not great. We end up with many nested callback functions that are dependent on the previous callback function. This is often referred to as a [callback hell](/016.%20Callback%20Hell/README.md), 

## ⭐ What is Promise ?

In Javascript, `Promise` is an object the represents **the eventual completion or failure of asynchronous operation and its resulting value.** Promises are a way to handle asynchronous operation more elegantly and avoid [callback hell](/016.%20Callback%20Hell/README.md) (nested callbacks) that can arise complex asynchronous scenarios.

> `Promise` placeholder for a value, until we receive a value from asynchronous operation.
`Promise` a container for a future value.


#### A Promise has three possible states:

* **Pending**: The initial state. The promise is neither fulfilled nor rejected.

* **Fulfilled**: The operation completed successfully, and the promise has a resulting value.

* **Rejected**: The operation encountered an error or failed, and the promise has a reason for the failure.

### ✨ Consider This example.

```js
const cart = ["shoes", "pants", "kurtas"];

api.createOrder(cart, function() {
    api.proceedToPayment(function() {
        api.showOrderSummary(function() {
            api.updateWallet();
        });
    });
});
```

Order of execution of callback function is depends on each other, which meansm when `createOrder` function execution completes, then proceeds to `proceedToPayment`, when this function execution completes then proceeds to `showOrderSummary`, when this function execution completes then proceeds to `updateWallet`.

**Issues**: 
* we are blindly trusting the function to executes the callback function.

* As we end up with tons of nested callback functions that make the code quite difficult to read

## ⭐ Promise Syntax

> "A promise is a placeholder for a value that can either resolve or reject at some time in the future"

![demo](/assets/demo24.gif)

A Promise is an object that contains a status, `([[PromiseStatus]])` and a value `([[PromiseValue]])`. In the above example, you can see that the value of [[PromiseStatus]] is "pending", and the value of the promise is undefined.

Don't worry - you'll never have to interact with this object, you can't even access the `[[PromiseStatus]]` and `[[PromiseValue]]` properties! However, the values of these properties are important when working with promises.

### ✨ The value of the PromiseStatus, the state, can be one of three values:

✅ **fulfilled**: The promise has been resolved. Everything went fine, no errors occurred within the promise 🥳

❌ **rejected** : The promise has been rejected. Argh, something went wrong..

⏳ **pending**: The promise has neither resolved nor rejected (yet), the promise is still pending.

## ⭐ `fetch()`

`fetch()` is a modern JavaScript API for making network requests (HTTP requests) in web browsers. It provides a more powerful and flexible way to interact with web servers compared to the older `XMLHttpRequest` (XHR) object. `fetch()` returns a Promise that resolves to the `Response` to that request, whether it is successful or not.


### ✨ Consider this Example

```js
const GITHUB_API = "https://api.github.com/users/itisameerkhan";
const user = fetch(GITHUB_API);
console.log(user);
```

In this example, 

when the code executed after **line:2** a `Promise` object is returned immediately with `[[PromiseStatus]] : 'Pending'` and `[[PromiseResult]] : undefined` and the code proceeds to the next line. 

![demo](/assets/demo25.png)

After sometime when the `Promise` object is Resolved either `fulfilled` or `rejected`.

In my case it resolved into `fulfilled`

![demo](/assets/demo26.png)
---

### ✨ `Promise {<pending>}`  but `state: fulfilled`?


When the code executed the `line:2` which returns a `Promise`, in this case which is in `pending` state. while the `Promise` being resolve, the code moves to `line:3`  to `console.log` the current state of the `Promise`. 

when the `Promise` is resolved after some time it replaced the `state: fulfilled` and `result: Response` in it. but not the `Promise {<pending>}` which is browser default behaviour.

---

### ✨ How to extract information from the `Promise` Object

## ⭐ `.then()`

The `.then()` method is part of the Promise API in JavaScript. It is used to attach callbacks that will be executed when a Promise is resolved. A Promise represents the eventual completion or failure of an asynchronous operation and allows you to handle the result once it's available.

```js
somePromise
  .then(onFulfilled)
  .catch(onRejected);
```

**somePromise**: The Promise object you want to handle.

**onFulfilled**: A callback function that will be executed when the Promise is successfully resolved. It takes the resolved value as an argument.

**.catch()**: A method that allows you to attach a callback to handle any rejection that might occur in the Promise chain. It takes a callback function as an argument, which is executed when the Promise is rejected.

### ✨ Consider This example

```js
const GITHUB_API = "https://api.github.com/users/itisameerkhan";

const user = fetch(GITHUB_API);

user.then(function(data) {
    console.log(data);
})
```
when we `console.log(data)` we get the `Response` of the `Promise`.

![dmeo](/assets/demo27.png)

`.then()` method invokes when the `Promise` is resolved successfully.

> `Promise` Object is immutable, which means it cannot be changed after resolved.

```js
const GITHUB_API = "https://api.github.com/users/itisameerkhan";

const user = fetch(GITHUB_API);

user.then(function(data) {
    return data.json();
})
.then(function(json) {
    console.log(json);
})
```
In this case, `response.json()` returns a `Promise` that resolves to the parsed JSON data, and the second `.then()` block handles that data.

![demo](/assets/demo28.png)

### ✨ How to avoid callback hell?

```js
const cart = ["shoes", "pants", "kurtas"];

api.createOrder(cart, function() {
    api.proceedToPayment(orderId, function() {
        api.showOrderSummary(paymentInfo, function() {
            api.updateWallet();
        });
    });
});
```

for that, 

```js
createOrder(cart).
then(function(orderId) {
    return proceedToPayment(orderId)
})
.then(function(paymentInfo) {
    return showOrderSummary(paymentInfo);
})
.then(function(paymentInfo) {
    return updateWallet(paymentInfo);
})
```

> To maintain `Promise` chaining, we need to `return` `Promise` from the `Promise`.

In this case, our code doesn't grow horizontally,

We can use `arrow` function also,

```js
createOrder(cart)
.then((orderId) => proceedToPayment(orderId))
.then((paymentInfo) => showOrderSummary(paymentInfo))
.then((paymentInfo) => updateWallet(paymentInfo));
```

## 🌐 Articles and Blogs

[⭐️🎀 JavaScript Visualized: Promises & Async/Await](https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke)