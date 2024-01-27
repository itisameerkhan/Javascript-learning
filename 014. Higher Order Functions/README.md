# 📈 Higher Order Functions (Functional Programming)

## What is Higher Order Function ? 

Higher Order function is a function which meets atleast one of the following criteria.

### 1. Takes function as a argument

```js
function x() {
    console.log("x function");
}

function y(x) {   // y is the higher order function
    x();
}
```

### 2. Return function as a argument

```js
function x() {
    return function() {
     console.log("function returns from another function");   
    }
}

const z = x();
z();
```

Higher-order functions are a fundamental concept in **functional programming**, and they provide a way to write more modular and reusable code. They enable you to pass behavior (functions) around, making your code more flexible and expressive.

--- 


### Consider this example 

#### 1. function to calculate area of a circle

```js
const radius = [1,2,3,4];

const calculateArea = function(radius) {
    const output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(Math.PI * radius[i] * radius[i]);
    }
    return output;
}

console.log(calculateArea(radius));
```

#### 2. function to calculate circumference of a cirlce

```js
const radius = [1,2,3,4];

const calculateArea = function(radius) {
    const output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(Math.PI * radius[i] * radius[i]);
    }
    return output;
}

const calculateCircumference = function(radius) {
    const output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(2 * Math.PI * radius[i]);
    }
    return output;
}

console.log(calculateCircumference(radius));
```

#### 3. Also includes diameter

```js
const radius = [1,2,3,4];

const calculateArea = function(radius) {
    const output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(Math.PI * radius[i] * radius[i]);
    }
    return output;
}

const calculateCircumference = function(radius) {
    const output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(2 * Math.PI * radius[i]);
    }
    return output;
}

const calculateRadius = function(radius) {
    const output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(radius[i] * radius[i]);
    }
    return output;
}

console.log(calculateRadius(radius));
```

> This is a valid program, but we need to write in more functional way. 
### Problems in this code

1. **Repeating**: all 3 functions have same functionality, but only thing changes is logic.



### Optimized Code

To make a code more optimized and more functional, we need to abstract function in which it is reusable not repeatable.

* The function which is abstract is `area`.

* We need generic function to maintain all execution, `calculate`.


```js
const radius = [1,2,3,4];

const area = function(radius) {
    return Math.PI * radius * radius;
}

const circumference = function(radius) {
    return 2 * Math.PI * radius;
}

const diameter = function(radius) {
    return radius * radius;
}

const caculate = function(radius, callback) {
    let output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(callback(radius[i]));
    }
    return output;
}

console.log(calculate(radius, area));
console.log(calculate(radius, circumference));
console.log(calculate(radius, diameter));
```

In this above code `calculate` is higher order function.

### Why we need Higher Order Function

1. Abstraction

2. Code Reusability

3. Flexibility

4. Functional Composition.

5. Callback Function

6. map, filter, reduce.

7. closure and state

8. currying

### Implementation of `map` behind

```js
const radius = [1,2,3,4];

const area = function(radius) {
    return Math.PI * radius * radius;
}

const circumference = function(radius) {
    return 2 * Math.PI * radius;
}

const diameter = function(radius) {
    return radius * radius;
}

Array.prototype.calculate = function(callback) {
    let output = [];
    for(let i=0;i<radius.length;i++) {
        output.push(callback(radius[i]));
    }
    return output;
}

console.log(radius.calculate(area));
```

### Extending Array Prototype:

The `calculate` method is added to the prototype of the `Array` object. This method takes a callback function (`callback`) as an argument and applies it to each element of the array (`radius`). The results are stored in an `output` array, which is then returned.