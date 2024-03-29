# 📍 Promise APIs

<img src='https://miro.medium.com/v2/resize:fit:1400/1*2Es3NVLS9PLb7d24TBZiGQ.png'>

In JavaScript promises, static methods are methods that are called on the Promise class itself rather than on an instance of a Promise. These static methods provide additional functionality for working with promises at a higher level. Here are the key static methods associated with the Promise class:

* **`Promise.all()`**
* **`Promise.allSettled`**
* **`Promise.race`**
* **`Promise.any`**

---

## ⭐ `Promise.all()`

Let’s say we want many promises to execute in parallel and wait until all of them are ready.


`Promise.all()` is a static method in JavaScript that takes an iterable (e.g., an array or other iterable object) of promises as input and returns a new promise. This new promise fulfills with an array of values when all the input promises have fulfilled, or it rejects with the reason of the first promise that rejects.

### ✨ Behaviour

#### ✒️ Fulfillment

If all promises in the iterable fulfill, the returned promise fulfills with an array containing the fulfillment values in the same order as the input promises.

#### ✒️ Rejection

If any promise in the iterable rejects, the returned promise rejects with the reason of the first promise that rejects. Subsequent rejections are ignored.

### ✨ Syntax

```js
Promise.all(iterable);
```

### ✨ Code snippet - All Success

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p1 success');
    }, 3000);
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p2 success');
    }, 1000);
})

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p3 success');
    }, 2000);
})

Promise.all([p1, p2, p3]).then((res) => { console.log(res) })
```

### output

![demo](/assets/demo37.png)


### ✨ Code snippet - if one promises fail

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p1 success');
    }, 3000);
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('p2 Failed');
    }, 1000);
})

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p3 success');
    }, 2000);
})

Promise.all([p1, p2, p3])
.then((res) => { console.log(res) })
.catch((err) => { console.error(err); })
```

![demo](/assets/demo38.png)

### ✨ consider this scenario. 

```js
Promise.all([p1, p2, p3])
```

In this above code p1, p2, p3 are promises trying to resolve,

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve.

* `p3`: takes 2 seconds to resolve.

### ✨ Success case ✅ 

If all of them are resolved(`fulfilled`)✅. `Promise.all()` returns array with response(result) of three promises. 

#### ✒️ Time taken

`Promise.all()` makes parallel promise calls and waits for all to be settled. so time taken in above code in 3 seconds.

### ✨ Failure case ❌: 

```js
Promise.all([p1, p2, p3])
```

In this above code p1, p2, p3 are promises trying to resolve,

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve. This promise gets **rejected**❌

* `p3`: takes 2 seconds to resolve.

1. In this above code, if any of the `promises` gets rejected `Promise.all()` will throw an error.

2.  What error this `Promise.all()` gets from rejected promise, it will returns the same error.

#### output: **ERROR**

> when it finds error in p2 which takes 1 seconds to resolved when it is found out error, it just simply throw error and not waits for other promises to resolve.

### ✨ Then what happened to p1 and p2?

Then what happened to p1 and p2, the response gets cancelled?
**NO**.

It is not possible to cancel promise execution from javascript.

**In simple word `Promise.all()` is all or none, if any one of Promise is failed all collective promise will fail**.

---

## ⭐ `Promise.allSettled()`


`Promise.allSettled()` is a static method introduced in ECMAScript 2020 (ES11/ES2020) for working with promises in JavaScript. It returns a promise that is fulfilled with an array of result objects for each promise in the input iterable (array or other iterable object). Each result object indicates whether the corresponding promise fulfilled or rejected, and includes the result or reason.

### ✨ Syntax 

```js
Promise.allSettled(iterable);
```

### ✨ Result Object 

Each result object in the array has the following properties:

* **status**: A string indicating the status of the promise, which can be either "fulfilled" or "rejected".

* **value**: The fulfillment value if the promise was fulfilled, or the rejection reason if the promise was rejected.

### ✨ Example 

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p1 success');
    }, 3000);
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('p2 Failed');
    }, 1000);
})

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p3 success');
    }, 2000);
})

Promise.allSettled([p1, p2, p3])
.then((res) => { console.log(res) })
.catch((err) => { console.error(err); })
```

![demo](/assets/demo39.png)

### ✨ Consider this example

```js
Promise.allSettled([p1, p2, p3]);
```
### ✨ Success case ✅ 

In this above code p1, p2, p3 are promises trying to resolve,

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve. 

* `p3`: takes 2 seconds to resolve.

After each Promises are fulfilled, then which returns response values or object.

### ✨ Failure case ❌: 

What if one of the Promise get rejected.

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve. rejected ❌

* `p3`: takes 2 seconds to resolve.

if `P2` was rejected after 1 seconds, it will not simply returns.

which will wait for the other 2 promises to resolve, then returns the fulfilled value or rejected message in the array after 3 seconds.

Irrespective of success or failure, it will give you all the results.

```js
[result1, error2, result3]
```

---

## ⭐ `Promise.race()`

`Promise.race()` is a static method in JavaScript that takes an iterable (e.g., an array) of promises as input and returns a new promise. This new promise settles (fulfills or rejects) as soon as one of the promises in the iterable settles. It resolves with the value or reason of the first settling promise.

> it can either be `fulfilled` or `rejected`, which comes first.

```js
Promise.allSettled([p1, p2, p3]);
```

### ✨ Code snippet 

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p1 success');
    }, 3000);
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('p2 Failed');
    }, 5000);
})

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p3 success');
    }, 2000);
})

Promise.race([p1, p2, p3])
.then((res) => { console.log(res) })
.catch((err) => { console.error(err); })
```

![demo](/assets/demo40.png)

### ✨ Success case ✅ 

In this above code p1, p2, p3 are promises trying to resolve,

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve. 

* `p3`: takes 2 seconds to resolve.

### Result 

which gives the value of `p2` which is resolved or settled **first**.

```js
VALUE FROM P2
```

### ✨ Failure case ❌: 

In this above code p1, p2, p3 are promises trying to resolve,

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve. ❌ **rejected**

* `p3`: takes 2 seconds to resolve.

### Result 

what if `p2` fails after 2 seconds, which will be returns error from the `p2`.   

output

```js
ERROR FROM P2
```

## ⭐ `Promise.any()`

`Promise.any()` is a static method of the Promise object introduced in ECMAScript 2021 (ES2021) that takes an iterable (like an array) of promises as input and returns a single new promise. Unlike `Promise.all()`, which waits for all input promises to settle (resolve or reject), `Promise.any()` fulfills when any of the input promises fulfills, with its fulfilled value. It rejects only if all input promises reject.

> It waits for the first promise to fulfill.

### ✨ Fulfillment:

* The returned promise resolves with the fulfilled value of the first promise to fulfill.

* It doesn't wait for other promises to settle after one fulfills.

### ✨ Rejection:

* The returned promise rejects with an `AggregateError` if all input promises reject. This error contains an array of rejection reasons from each rejected promise.

```js
Promise.any([p1, p2, p3]);
```

### ✨ Code snippet 

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p1 success');
    }, 3000);
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('p2 Failed');
    }, 1000);
})

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('p3 success');
    }, 2000);
})

Promise.any([p1, p2, p3])
.then((res) => { console.log(res) })
.catch((err) => { console.error(err); })
```

![demo](/assets/demo41.png)

### ✨ what if all promises are rejected

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        // resolve('p1 success');
        reject('p1 failed');
    }, 1000);
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('p2 failed');
        // resolve('p2 success');
    }, 1000);
})

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        // resolve('p3 success');
        reject('p3 failed');
    }, 1000);
})

Promise.any([p1, p2, p3])
.then((res) => { console.log(res) })
.catch((err) => { console.error(err); })
```
![demo](/assets/demo42.png)

### ✨ Success case ✅ 

In this above code p1, p2, p3 are promises trying to resolve,

* `p1`: takes 3 seconds to resolve.

* `p2`: takes 1 seconds to resolve. 

* `p3`: takes 2 seconds to resolve.

**output: value of p2**

if `p2` gets rejected, it waits for another promise to success.
which is `p3`. if `p3` is failed again it wait for another success which is `p1`.

if All promises are rejected, then returns `AggregateError`.
which is array of all error [error1, error2, error3].