# 📍 Async & Await 

<img src='https://miro.medium.com/v2/resize:fit:2000/1*a25_oLG-cts9PvIckJo1GQ.png' >

---

ES7 introduced a new way to add `async` behavior in JavaScript and make working with promises easier! With the introduction of the `async` and `await` keywords, we can create `async` functions which implicitly return a promise. 

Previously, we saw that we can explicitly create promises using the Promise object, whether it was by typing `new Promise(() => {})`, `Promise.resolve`, or `Promise.reject`.

Instead of explicitly using the `Promise` object, we can now create asynchronous functions that implicitly return an object! This means that we no longer have to write any Promise object ourselves.

Although the fact that `async` functions implicitly return promises is pretty great, the real power of `async` functions can be seen when using the `await` keyword! With the `await` keyword, we can suspend the asynchronous function while we wait for the `await`ed value return a resolved promise. If we want to get the value of this resolved promise, like we previously did with the `then()` callback, we can assign variables to the `await`ed promise value!

<img src='https://res.cloudinary.com/practicaldev/image/fetch/s--5ED_HyNC--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/72lqrcvy9lc8ehbpitd0.png'>


## ⭐ `async` Function

**The `async` keyword is used to declare a function as asynchronous. An asynchronous function always returns a `Promise`, and it allows the use of the `await` keyword within its body.**

> Either you can return a promise from this function, when you return somehing else automatically this function wraps the result into the promise and return a promise.

```js
async function getData() {
    return "Namaste";
}

const data = getData();
console.log(data);
```

![demo](/assets/demo43.png)

#### ✒️ How to get the actual data using `.then()`
> Not recommended

```js
async function getData() {
    return "Namaste";
}

const dataPromise = getData();

dataPromise.then(res => { console.log(res); })
```
### output

```
Namaste
```

#### ✒️ Another Example

```js
const p = new Promise((resolve, reject) => {
    resolve('Promise resolved value');
})

async function getData() {
    return p;
}

const dataPromise = getData();

dataPromise.then(res => { console.log(res); })
```

What if return promise from `async` function will it wraps into another promise an returns. **NO**. It returns the Promise.


## ⭐  `await` Operator

The `await` keyword is used to pause the execution of an asynchronous function until the Promise is resolved, and it returns the resolved value.

> 📝 `await` keyword is only being used inside the `async` function. `await` used before the Promise.

```js
const p = new Promise((resolve, reject) => {
    resolve('Promise resolved value');
})

async function handlePromise() {
    const result = await p;
    console.log(result);
} 

handlePromise();
```

### 💻 Output

```
Promise resolved value
```

### ✨ Using `await` with the Promise

```js
const result = await p;
```

Inside the `handlePromise` function, the `await` keyword is used to pause the execution until the Promise `p` is resolved. The resolved value is then stored in the variable result.

## ⭐ A Key Difference between `then()` and `async/await`.

### ✨ `.then()`

`.then()` involves chaining methods, which can lead to a pattern known as "callback hell" when dealing with multiple asynchronous operations. This can result in deeply nested code, making it harder to read and maintain.

```js
fetchData()
  .then((result) => {
    return processResult(result);
  })
  .then((processedResult) => {
    console.log(processedResult);
  })
  .catch((error) => {
    console.error(error);
  });
```

### ✨ `async/await`

`async/await` provides a more synchronous-like syntax, making the code appear sequential and enhancing readability. It allows you to write asynchronous code in a way that resembles synchronous code, making it easier to understand.

```js
async function fetchDataAsync() {
  try {
    const result = await fetchData();
    const processedResult = await processResult(result);
    console.log(processedResult);
  } catch (error) {
    console.error(error);
  }
}

fetchDataAsync();
```

### ✨ Consider this example using `.then()`

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise resolved value');
    },5000);
});

function getData() {
    p.then((res) => console.log(res));
    console.log('Namaste Javascript');
}

getData();
```

### ✨ Breakdown

* When `getData` function is called, `Promise` `p` is initiated with Timer which is register in WebAPIs

* JS engine is not wait for promise to be resolved, it will proceed to next line of code to execute.

* When the `Promise` is resolved, which is then push the resolved value in **Microtask queue**.

* `.then()` has a callback function which is executed when the `Promise` is resolved. 

* After 5 seconds, Event Loop which checks for the empty **callstack** and something inside **microtask queue**. which is then pushed into callstack and started executing.

```
Namaste Javascript
Promise resolved value
```

### ✨ Consider this example using `async/await`

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise resolved value');
    },5000);
});


async function handlePromise() {
    const result = await p;
    console.log('Namaste Javascript');
    console.log(result);
} 

handlePromise();
```

### 💻 Output 

```
Namaste Javascript 
Promise resolved value
```

### ✨ Execution Details

* When `handlePromise` is called, it starts executing its code.
The `await` `p` statement **pauses the execution of the function until the Promise (p) is resolved**. During this pause, control is returned to the **event loop**, allowing other asynchronous tasks to run.

* After the 5000 milliseconds delay, the Promise is resolved, and pushes into microtask queue. which is executed after callstack is empty. and the function resumes execution by event loop.

* The message '`Namaste Javascript`' is logged to the console.

* The `result` variable now holds the resolved value of the Promise, which is logged to the console.

### 💻 Consider this example

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise resolved value');
    },5000);
});


async function handlePromise() {
    console.log('something - 1');
    const result = await p;
    console.log('something - 2');
    console.log(result);
} 

console.log('something - 3');
handlePromise();
console.log('something - 4');
```

### 💻 Output

```
something - 3
something - 1
>>> (after 5 seconds)
something - 4
something - 2
Promise resolved value
```

### 💻 Consider this example

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise resolved value');
    },5000);
});


async function handlePromise() {
    console.log('something - 1');
    const result = await p;
    console.log('something - 2');
    console.log(result);   
    
    const result2 = await p;
    console.log('something - 3');
    console.log(result2);    
} 

console.log('something - 4');
handlePromise();
console.log('something - 5');
```

### 💻 OUTPUT

```
something - 4
something - 1
something - 5
>>> (after 5 seconds)
something - 2
Promise resolved value
something - 3
Promise resolved value
```