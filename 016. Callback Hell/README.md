# 💫 Callback 

![demo](/assets/demo21.png)

Consider cart items in javascript.

* once we have the cart items, steps need to follow are 

    1. **create order**
    2. **payment**


```js
const cart = ["shoes", "pants", "kurtas"];

api.createOrder();

api.proceedToPayment();
```

**In this asynchronous code, we need dependencies to the execution.** which means when the function `createOrder` is executed afterwards the function `proceedToPayment` function should execute.

--- 
To fix this **callback** function comes into picture.


```js
const cart = ["shoes", "pants", "kurtas"];

api.createOrder(cart, function() {
    api.proceedToPayment();
});
```

### Explanation

1. `createOrder` function is an asynchronous operation that takes some time to complete, therefore we are using **callback** function to ensure that the call to `proceedToPayment` happens only after the order creation is complete.

### Breakdown

1. `api.createOrder` function is called with the `cart` array and a callback function as an argument.

2. The callback function is execute after the order creation is complete.

---

### Add another feature **OrderSummary**



```js
const cart = ["shoes", "pants", "kurtas"];

api.createOrder(cart, function() {
    api.proceedToPayment(function() {
        api.showOrderSummary();
    });
});
```
### Explanation

* when the `createOrder` function execution completes, then proceeds to `processToPayment`.

* when `proceedToPayment` function execution completes, then proceeds to `showOrderSummary`.

---

### Add another feature **updateWallet**


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

### Explanation

* when the `createOrder` function execution completes, then proceeds to `processToPayment`.

* when `proceedToPayment` function execution completes, then proceeds to `showOrderSummary`.

* when `showOrderSummary` function execution completes, then proceeds to `updateWallet` and this callback function goes on.




## Problem on the above code 

* callback function execution one after another makes the code grow horizontally instead of vertically.

* This code is hard to readable and unmaintainable.

## ✨ What is Callback Hell?

Callback hell, also known as **"pyramid of doom"** or **"callback spaghetti,"** refers to a situation in JavaScript programming where multiple nested callbacks make the code hard to read, understand, and maintain. This typically occurs in asynchronous operations, **where one function or operation is depending on each other.** the code structure becomes deeply nested and hard to follow.

 This typically occurs when dealing with **asynchronous** operations, such as making API requests or handling file I/O, **where one operation depends on the result of another or previous One.**


## 💫 Risk on Callback Functions

```js
const cart = ["shoes", "pants", "kurtas"];

api.createOrder(cart, function() {
    api.proceedToPayment();
});
```

* In this code, `proceedToPayment` is important piece of code. we gave the control of our operation to `createOrder` api. now its the `createOrder` api responsibility to call our function. we are blindly trusting. 

* what if, we may encountered bugs in `createOrder`, or what if callback function is never called ?. because we don't know what written inside `createOrder` api, what if `proceedToPayment` called twice.

* while we giving callback function, we give responsible to `createOrder` function to execute.

---

## 💫 Two issues while using callbacks

### 1 - Callback hell

When a function is passed as an argument to another function, it becomes a callback function. This process continues and there are many callbacks inside another's Callback function.
This grows the code horizontally instead of vertically. That mechanism is known as callback hell. 

### 2 - Inversion of control

The callback function is passed to another callback, this way we lose the control of our code. We don't know what is happening behind the scene and the program becomes very difficult to maintain. 
That process is called inversion of control. 


## 💫 Escaping callback Hell

**To escape callback hell, Javascript developer adopted various techniques and patterns**

1. **🔥 1. Promises to the Rescue**

2. **🔥 2. Embrace the Power of Async/Await**


## 🌐 Articles 

* [Callback Hell in JavaScript : All You Need to Know](https://medium.com/@raihan_tazdid/callback-hell-in-javascript-all-you-need-to-know-296f7f5d3c1)