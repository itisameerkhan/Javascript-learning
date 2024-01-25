## Block Statement

  In JavaScript, a block statement is a group of statements enclosed in curly braces `{}`. It is used to group multiple statements together into a single compound statement. A block statement can be used wherever a single statement is expected.

 ```js
 {
  // statement 1
  // statement 2
  // ...
  // statement n
}
 ```

 ### Block Scope

 The variables and functions that can be accessed inside block statement. 

 ```js
 {
  var a = 10;
  let b = 20;
  const c = 30;
 }
 console.log(a); // 10
 console.log(b); // Uncaught ReferenceError: Cannot access 'b' from debugger
 console.log(c); // Uncaught ReferenceError: Cannot access 'c' from debugger
 ```

 ![demo](/assets/dem11.png)

 ### Shadowing in JS

 
In JavaScript, shadowing occurs when a variable declared within a certain scope has the same name as a variable in an outer scope. The inner variable **shadows** the outer variable, making the outer variable temporarily inaccessible within the inner scope.

```js
var a = 10;
{
  var a = 100;
}
console.log(a) // 100
```

```js 
let a = 10;
const b = 20;
{
  let a = 100;
  const b = 200;
}
console.log(a) // 10;
console.log(b) // 20
```

### Illegal shadowing 

```js
var a = 10;
{
  let a = 10; ✅
}
```

```js
let a = 10;
{
  var a = 10; ❌ // SyntaxError: Identifier 'a' has already been declared
}
```
```js
let a = 10;
{
  let a = 20; ✅
}
```

### Lexical Scope Chain 

```js
const a =  10;
{
  const a = 10;
  {
    const a = 10;
  }
}
```

![demo](/assets/demo8.png)
