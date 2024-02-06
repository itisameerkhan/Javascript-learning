# 📍 `This` Keyword

<img src='https://www.freecodecamp.org/news/content/images/2023/01/brad-_Js9c6w_FDk-unsplash.jpg' >

In JavaScript, the `this` keyword refers to the context in which a function is executed. Its value depends on how a function is called.

## ⭐ `this` in Global Space

In the global context of JavaScript, outside of any function, the `this` keyword refers to the `global` object. In a web browser environment, the global object is typically `window`, while in Node.js, it's `global`.

### 💻 Demo code

```js
console.log(this);
```

### 💻 output

![demo](/assets/demo49.png)


### 💻 Demo code

```js
console.log(this === window)
```

### 💻 Output

```js
true
```

## ⭐ `this` inside a function

When a function is invoked as a standalone function, this refers to the `global` object in `non-strict` mode. In `strict mode`, it's `undefined`.

### 💻 Example

```js
console.log(this);

function fun() {
    console.log(this);
}

fun();
```

### 💻 Output 

> [!NOTE]
> Non strict mode

![demo](/assets/demo50.png)

### 💻 Example

```js
'use strict'

console.log(this);

function fun() {
    console.log(this);
}

fun();
```

### 💻 Output 

> [!NOTE]
> strict mode

![demo](/assets/demo51.png)

## ⭐ `this` is strict mode - (This Substitution)

In **strict mode**, the behavior of the `this` keyword is slightly different compared to **non-strict mode**. In particular, when a function is invoked as a standalone function (i.e., not as a method of an object), the value of `this` inside the function is not automatically bound to the `global` object as it is in **non-strict mode**. Instead, it retains its initial value of `undefined`.

This behavior is often referred to as **"this substitution"** in **strict mode**. It means that when a function is called without any context, this is not implicitly assigned to the `global` object. This can help prevent accidental modification of `global` variables and improve code safety.

>[!NOTE]
> If the value of `this` keyword is undefined or null. `this` keyword will be replaced with `global` object only in non strict mode.

### 💻 Example

```js
'use strict';

function myFunction() {
  console.log(this); 
}

myFunction();
```

### 💻 Output 

```
undefined
```

## ⭐ `this` keyword value depends on how `this` is called (`window`)

### 💻 Example

```js
"use strict"

function fun() {
    console.log(this);
}

fun();
window.fun();
```

![demo](/assets/demo51.png)

#### `fun();` 

Calls the `fun` function. Without any context, `this` inside the function refers to the global object (window in browsers).

### `window.fun();` 

Calls the `fun` function explicitly on the `window` object. In this case, this inside the function also refers to the window object.

However, in strict mode **("use strict")**, calling a function without any context (`fun()`) will set this to `undefined` instead of the `global` object. Therefore, in **strict mode**, `this` inside the `fun` function will be `undefined` when invoked directly (`fun()`). This can help prevent unintentional global variable modifications and enhance code safety.

## ⭐ `this` inside a object's method


In JavaScript, when a method is invoked on an object, the `this` keyword inside that method refers to the **object** on which the method is called. This behavior allows methods to access and operate on the properties of the object they belong to.

### 💻 Example

```js
const obj = {
    a: 10,
    fun: function() {
        console.log(this);
    }
}

obj.fun()
```

### 💻 output

```
{a: 10, x: ƒ}
```

### 💻 Example

```js
const obj = {
    a: 10,
    fun: function() {
        console.log(this.a);
    }
}

obj.fun()
```

### 💻 output

```
10
```

## ⭐ `call`, `bind`, `apply` methods(sharing methods)

In JavaScript, `call`, `apply`, and `bind` are methods that allow you to control the value of this in function invocations. They provide a way to explicitly set the context (the value of this) when calling a function. 

### ✨ `call`

The `call` method is used to invoke a function with a specified `this` value and optional arguments provided individually.

### 💻 Example 

```js
const student1 = {
    name: "Khan",
    printName: function() {
        console.log(this.name);
    },
}

const student2 = {
    name: "Rose",
}

student1.printName();
student1.printName.call(student2);
```

### 💻 output

```
khan 
Rose
```

## ⭐ `this` keyword inside arrow function

In JavaScript, arrow functions (`=>`) behave differently with respect to the `this` keyword compared to regular functions. The main difference is that arrow functions do not have their own `this` context; instead, they **lexically capture the value of `this` from the surrounding lexical scope**

> [!NOTE]
> arrow functions don't provide their own `this` binding (it retains the `this` value of the enclosing lexical context).

### 💻 Example

```js
const obj = {
    a: 10,
    x: () => {
        console.log(this);
    }
}

obj.x();
```

### 💻 Output

![demo](/assets/demo49.png)

### ✨ Lexical Scope Binding

Unlike regular functions, arrow functions do not bind their own `this` context. Instead, they inherit the value of `this` from the enclosing lexical scope at the time of their definition.

### ✨ Common Use Cases

Arrow functions are commonly used in callback functions, event handlers, and asynchronous code (e.g., with promises and async/await) where the lexical `this` behavior simplifies code and avoids the need for manual `this` binding or workarounds like storing `this` in a separate variable (`const self = this`).

### 💻 Example

```js
const obj   = {
    a: 10,
    x: function() {
        const y = () => {
            console.log(this);
        }
        y();
    }
}

obj.x();
```

### 💻 Output

```
{a: 10, x: ƒ}
```

## ⭐ `this` inside DOM

In JavaScript, the behavior of the `this` keyword in the context of the Document Object Model (DOM) depends on how and where a function is invoked within event handlers, event listeners, and other DOM-related contexts. 

### ✨ Event Handlers

In event handler attributes (e.g., `onclick`, `onmouseover`) within HTML elements, this refers to the DOM element that triggered the event. For example, in an `onclick` attribute, this refers to the element being clicked.

> ![NOTE]
> reference to HTML element

### 💻 Example

```js
const button = document.querySelector('button');

button.addEventListener('click',handleClick);

function handleClick() {
    console.log(this);
    console.log(this.id);
    console.log(this.tagName);
}
```

### 💻 Output

```html
<button id="btn"></button>
btn
BUTTON
```
