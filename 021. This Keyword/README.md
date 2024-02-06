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