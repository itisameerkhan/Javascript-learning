# Undefined Not-defined Null

 * `undefined`:  In JavaScript, `undefined` is a primitive value and a type. It indicates that a variable has been declared but has not been assigned a value. Additionally, it can be the default value of function parameters that are not provided.

 ```js
  var x; 
  typeof(x) // undefined
 ```
---
* `not defined`: The term "not defined" is often used when a variable or identifier is used without being declared at all. This results in a ReferenceError.

```js
console.log(x) // ReferenceError: x is not defined
```

```js 
null == undefined // true 
null === undefined // false
```

---

 * `null`: assignment value given to a variable. The variable which has been assigned to `null` has no value.
 * When we assign null as a value to any variable, it means that it is empty or blank. It is to show that the variable has no value.
 * Also, null is an **object** in JavaScript. 

 ```js
 var x = null
 typeof(null) // object
 ```
