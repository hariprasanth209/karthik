
---

#  Function Declaration

## Syntax

```js
function greet(name) {
  return "Hello " + name;
}
```

## Call

```js
greet("Sam");
```

---

##  Hoisting Behavior

Function declarations are hoisted.

```js
sayHi();   //  Works

function sayHi() {
  console.log("Hi");
}
```

They are loaded into memory before execution.

---

#  Function Expression

A function stored inside a variable.

```js
const greet = function(name) {
  return "Hello " + name;
};
```

---

##  Not Hoisted

```js
greet("Sam"); // X(NO) Error

const greet = function(name) {
  return "Hello " + name;
};
```

Because variables with `const/let` are in TDZ.

---

#  Difference

| Feature           | Declaration | Expression |
| ----------------- | ----------- | ---------- |
| Hoisted           | Yes         | No         |
| Can be anonymous  | No          | Yes        |
| Used in callbacks | Rare        | Common     |

---

#  Arrow Functions (ES6)

Shorter syntax. No own `this`.

## Basic

```js
const greet = (name) => {
  return "Hello " + name;
};
```

---

## Implicit return (one line)

```js
const greet = name => "Hello " + name;
```

---

## Multiple parameters

```js
const add = (a, b) => a + b;
```

---

## No parameter

```js
const sayHi = () => "Hi";
```

---

##  Important: Arrow does NOT bind its own `this`

In React & callbacks → preferred
In object methods → be careful

---

#  Default Parameters

```js
function greet(name = "Guest") {
  return "Hello " + name;
}
```

```js
greet();        // Hello Guest
greet("Sam");  // Hello Sam
```

---

#  Rest & Spread Operators

Both use `...` but behave differently.

---

##  Rest Operator (Collect values)

Used in function parameters.

```js
function sum(...numbers) {
  return numbers.reduce((acc, val) => acc + val, 0);
}
```

```js
sum(1, 2, 3, 4); // 10
```

It converts arguments into an array.

---

##  Spread Operator (Expand values)

### Array

```js
let arr1 = [1, 2];
let arr2 = [...arr1, 3, 4];
```

### Object

```js
let user = { name: "Sam" };
let updated = { ...user, age: 27 };
```

---

##  MERN Use Case

Updating state in React:

```js
setUser({ ...user, name: "New Name" });
```

---

#  Higher-Order Functions (Very Important)

A function that:

* Takes another function as argument
  OR
* Returns another function

---

## Example 1 – Takes function

```js
function operate(a, b, operation) {
  return operation(a, b);
}

function add(x, y) {
  return x + y;
}

operate(5, 3, add); // 8
```

---

## Example 2 – Returns function

```js
function multiplier(x) {
  return function(y) {
    return x * y;
  };
}

const double = multiplier(2);
double(5); // 10
```

---

##  Real MERN Examples

* `map()`
* `filter()`
* `reduce()`
* Express middleware
* React hooks

---

#  Callback Functions

A function passed as argument and executed later.

---

## Example

```js
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

function sayBye() {
  console.log("Bye");
}

greet("Sam", sayBye);
```

---

## Asynchronous Example

```js
setTimeout(() => {
  console.log("Runs after 2 seconds");
}, 2000);
```

Arrow function is callback.

---

##  Callback Hell

Nested callbacks become unreadable:

```js
doSomething(function() {
  doAnother(function() {
    doMore(function() {
    });
  });
});
```

This is why Promises and async/await exist.

---

#  Pure Functions

A function is pure if:

1. Same input → same output
2. No side effects
3. Does not modify external state

---

## Pure Example

```js
function add(a, b) {
  return a + b;
}
```

---

## Impure Example

```js
let total = 0;

function add(num) {
  total += num;   // modifies external variable
}
```

---

## Why Pure Functions Matter?

* Predictable
* Easy to test
* Used heavily in React
* Better debugging

---

#  MERN-Level Understanding

You must clearly understand:

* Why arrow functions are preferred in React
* Why higher-order functions power array methods
* Why pure functions improve maintainability
* Why callbacks are foundation of async JS
* Why rest/spread is critical in state updates

---

# Interview-Level Questions You Should Answer

1. Difference between function declaration & expression?
2. Why arrow functions behave differently with `this`?
3. What is higher-order function?
4. What is callback hell?
5. What makes a function pure?

---

