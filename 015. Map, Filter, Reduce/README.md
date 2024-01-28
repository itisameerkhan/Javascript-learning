# Map, Filter, Reduce 

![demo](/assets/demo20.png)

Map, Filter, Reduce are [Higher Order Function](/014.%20Higher%20Order%20Functions/README.md)


## Map

**`map` method creates new array by applying provided function to each element of the original array.**

`map` method used to transform the each element in the original array.

#### Double the value in array

```js
const arr = [1,2,3,4,5];

function double(x) {
    return 2 * x;
}

const output = arr.map(double);

console.log(output);
```

### output

```
[2,4,6,8,10]
```

#### Find Binary of each element

```js
const arr = [1,2,3,4,5];

function binary(x) {
    return x.toString(2);
}

const output = arr.map(binary);

console.log(output);
```

### output

```
["1","10","11","100","101"]
```

---

## Filter

**The `filter` method creates a new array with all elements that pass a provided condition.**

`Filter` method is used to filter element in an array, with respect to condition in callback function.

#### Filter out even number in array

```js
const arr = [1,2,3,4,5];

function isOdd(x) {
    return x % 2;
}

const output = arr.filter(isOdd);

console.log(output);
```

### output

```
[1,3,5]
```

#### Alternative which is valid callback function

```js
const arr = [1,2,3,4,5];

const output = arr.filter(function(x) {
    return x % 2;
});

console.log(output);
```

```js
const arr = [1,2,3,4,5];

const output = arr.filter((x) => {
    return x % 2;
});

console.log(output);
```

```js
const arr = [1,2,3,4,5];

const output = arr.filter((x) => return x % 2; );

console.log(output);
```

---

## Reduce

**The reduce method applies a function against an `accumulator` and each `element` in the array (from left to right) to reduce it to a single value.**

`reduce` method used where we have take all elements in an array and comes with single value out of them.

```js
const result = nums.reduce((accumulator, element, index, array) => {

}, initialValue)
```

#### Find sum of the array

```js
const nums = [1,2,3,4,5];

const output = nums.reduce((accumulator, element) => {
    return accumulator += element;
})

console.log(output);
```

#### output

```
15
```

* **accumulator**: used to accumulate the result of each values.

* **element**: represents the current value of the array

#### Find maximum value of array

```js
const nums = [1,2,3,4,5];

const output = nums.reduce((accumulator, element) => {
    if(element > accumulator) {
        accumulator = element;
    }
    return accumulator;
},0)

console.log(output);
```

#### output

```
5
```

---

#### 1. Find list of Full name

#### output

```
["akshay saini", "donald trump", "deepika padukone"]
```

#### code

```js
const users = [
    {firstName: "akshay", lastName: "saini", age: 26},
    {firstName: "donald", lastName: "trump", age: 75},
    {firstName: "elon", lastName: "musk", age: 50},
    {firstName: "deepika", lastName: "padukone", age: 26},
];

const output = users.map((data) => data.firstName + " " + data.lastName);

console.log(output);
```

#### 2. combine users with same age category

#### output

```
{ 26: 2, 50: 1, 75: 1}
```

#### Code 

```js
const users = [
    {firstName: "akshay", lastName: "saini", age: 26},
    {firstName: "donald", lastName: "trump", age: 75},
    {firstName: "elon", lastName: "musk", age: 50},
    {firstName: "deepika", lastName: "padukone", age: 26},
];

const output = users.reduce((acc, curr) => {
    if(acc[curr.age]) {
        acc[curr.age]++;
    } else {
        acc[curr.age] = 1;
    }
    return acc;
}, {});

console.log(output);
```

#### 3. Find firstName of users where age is below 30

```js
const users = [
    {firstName: "akshay", lastName: "saini", age: 26},
    {firstName: "donald", lastName: "trump", age: 75},
    {firstName: "elon", lastName: "musk", age: 50},
    {firstName: "deepika", lastName: "padukone", age: 26},
];

const output = users.filter((data) => data.age < 30).map((data) => data.firstName);

console.log(output);
```

#### Output

```
[ "akshay", "deepika" ]
```

#### Same code with `reduce`

```js
const users = [
    {firstName: "akshay", lastName: "saini", age: 26},
    {firstName: "donald", lastName: "trump", age: 75},
    {firstName: "elon", lastName: "musk", age: 50},
    {firstName: "deepika", lastName: "padukone", age: 26},
];

const output = users.reduce((acc, curr) => {
    if(curr.age < 30) {
        acc.push(curr.firstName);
    }
    return acc;
},[]);

console.log(output);
```

#### output

```
["akshay", "deepika"]
```