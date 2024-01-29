# 💫 Creating a Promise

![demo](/assets/demo24.gif)

A Promise is an object that contains a status, `([[PromiseStatus]])` and a value `([[PromiseValue]])`. In the above example, you can see that the value of `[[PromiseStatus]]` is "**pending**", and the value of the promise is **undefined**.

Don't worry - you'll never have to interact with this object, you can't even access the `[[PromiseStatus]]` and `[[PromiseValue]]` properties! However, the values of these properties are important when working with promises.

### The value of the PromiseStatus, the state, can be one of three values:

✅ **fulfilled**: The promise has been resolved. Everything went fine, no errors occurred within the promise 🥳

❌ **rejected** : The promise has been rejected. Argh, something went wrong..

⏳ **pending**: The promise has neither resolved nor rejected (yet), the promise is still pending.

### ✨ when is a promise status "pending", "fulfilled" or "rejected"? And why does that status even matter?

In the above example, we just passed the simple callback function `() => {}` to the Promise constructor. However, this callback function actually receives two arguments. The value of the first argument, often called `resolve` or `res`, is the method to be called when the Promise should resolve. The value of the second argument, often called `reject` or `rej`, is the value method to be called when the Promise should reject, something went wrong.

![demo](/assets/demo29.png)

Let's try and see that gets logged when we invoke either the `resolve` or `reject` method! In my example, I called the resolve method `res`, and the reject method `rej`.

![demo](/assets/demo30.gif)

Awesome! We finally know how to get rid of the "`pending`" status and the `undefined` value! The status of a promise is "`fulfilled`" if we invoked the `resolve` method, and the status of the promise is "`rejected`" if we invoked the `rejected` method.

The `value` of a promise, the value of `[[PromiseValue]]`, is the value that we pass to the either the resolved or rejected method as their argument.

But... what now? We don't care about that entire promise object, we only care about the value of the data! Luckily, there are built-in methods to get a promise's value. To a promise, we can attach 3 methods:

* `.then()`: Gets called after a promise resolved.

* `.catch()`: Gets called after a promise rejected.

* `.finally()`: Always gets called, whether the promise resolved or rejected.

![demo](/assets/demo33.png)

> FYI, when you know that a promise will always resolve or always reject, you can write Promise.resolve or Promise.reject , with the value you want to reject or resolve the promise with!

![demo](/assets/demo34.png)

---

### ✨ Consider this example

```js
const cart = ["shorts", "pants", "kurta"];

const promise = createOrder(cart); // async operation which return Promise


promise.then(function(orderId) {
    console.log(orderId);
    // proceedToPayment(orderId)
})

// Producer

function createOrder(cart) {
    return new Promise(function(resolve, reject) {
        // create on order
        // validate cart
        if(!validateCart(cart)) { // Reject a Promise
            const err = new Error("cart is not valid");
            reject(err);
        } 
        const orderId = [1,2,3];
        if(orderId) { // Resolve a Promise
            setTimeout(function() {
                resolve(orderId);
            }, 5000);
        }
    })
}

function validateCart(cart) {
    return true;
}
```

In this example `createOrder` function is a async operation that returns `Promise` object.

* `resolve(orderId)`: To `fulfilled` the status and gets the results of the promise.

* `reject(err)`: To `rejected` the status and get the results as error message.

### ✨ `resolve()` message

![demo](/assets/demo31.png)

### ✨ `reject()` message

```js
function validateCart(cart) {
    return false;
}
```

![demo](/assets/demo32.png)

We get this error as "**cart is not valid**". but we want to handle this error message using `catch()`

### ✨ `catch()`

```js
const cart = ["shorts", "pants", "kurta"];
const promise = createOrder(cart); 

promise.then(function(orderId) {
    console.log(orderId);
})
.catch(function(err) {
    console.log(err.message);
}) 

function createOrder(cart) {
    return new Promise(function(resolve, reject) {
        if(!validateCart(cart)) { // Reject a Promise
            const err = new Error("cart is not valid");
            reject(err);
        } 
        const orderId = [1,2,3];
        if(orderId) { // Resolve a Promise
            setTimeout(function() {
                resolve(orderId);
            }, 5000);
        }
    })
}

function validateCart(cart) {
    return false;
}
```

### output

```
cart is not valid
```

# 💫 Promise Chaining

In the `cart` example, we ended up having to nest multiple callbacks in order to run them. Luckily, the `.then` handlers can help us with that! 🥳

The result of the `.then` itself is a promise value. This means that we can chain as many **.thens** as we want: the result of the previous then callback will be passed as an argument to the next then callback!

> we need to **return** any value or another `Promise` from one chain to another.

![demo](/assets/demo35.png)

### ✨ Consider this example on `Promise` chaining

```js
const cart = ["shorts", "pants", "kurta"];

createOrder(cart)
.then(function(orderId) {
    return orderId;
})
.then(function(orderId) {
    return proceedToPayment(orderId);
})
.then(function(paymentInfo) {
    console.log(paymentInfo);
})
.catch(function(err) {
    console.log(err.message);
});

function createOrder(cart) {
    return new Promise(function(resolve, reject) {
        if(!validateCart(cart)) { 
            const err = new Error("cart is not valid");
            reject(err);
        } 
        const orderId = [1,2,3];
        if(orderId) { 
            setTimeout(function() {
                resolve(orderId);
            }, 5000);
        }
    })
}

function proceedToPayment(orderId) {
    return new Promise(function(resolve, reject) {
        resolve("payment successful");
    })
}

function validateCart(cart) {
    return true;
}
```

> we cannot `resolve` or `reject` Promise twice.


### ✨ `Promise` chain using Arrow function

```js
createOrder(cart)
.then(orderId => orderId)
.then(orderId => proceedToPayment(orderId))
.then(paymentInfo => updateWallet(paymentInfo))
.catch(err => { console.log(err) });
```

### ✨ Suppose I want to execute `catch()` before `proceedToPayment()`

```js
createOrder(cart)
.then(function(orderId) {
    return orderId;
})
.catch(function(err) {  // catch - 1
    console.log(err.message);
});
.then(function(orderId) {
    return proceedToPayment(orderId);
})
.then(function(paymentInfo) {
    console.log(paymentInfo);
})
```

`catch()` on the above **catch - 1** catches `reject` above `.then()` methods, not below.

> If there is `.then()` method after `.catch()`. then `.then()` will be definitely called.

```js
createOrder(cart)
.then(function(orderId) {
    return orderId;
})
.then(function(orderId) {
    return proceedToPayment(orderId);
})
.catch(function(err) { 
    console.log(err.message);
});    
.then(function(paymentInfo) {
    console.log("iam definitely called no matter what");
})
```

