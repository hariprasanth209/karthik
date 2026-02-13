
---

#  Global Scope

A variable declared outside any function or block belongs to global scope.

```js
let name = "Sam";

function greet() {
  console.log(name);
}

greet(); // Sam
```

### Properties:

* Accessible everywhere
* Exists for entire program lifetime
* In browser → attached to `window`
* In Node → not attached to global automatically (ES modules)

---

##  Problem with Global Variables

* Hard to track changes
* Risk of overwriting
* Makes debugging difficult

Best practice:
Keep globals minimal.

---

#  Function Scope

Variables declared inside a function are accessible only inside that function.

```js
function test() {
  let x = 10;
  console.log(x);
}

test();
console.log(x); // X(NO) Error
```

Each function creates its own scope.

---

#  Block Scope

Introduced in ES6 using `let` and `const`.

Blocks are:

* if
* for
* while
* {}
* switch

```js
if (true) {
  let x = 20;
  const y = 30;
}

console.log(x); // X(NO) Error
```

---

## Important Difference: var vs let

```js
if (true) {
  var a = 10;
}

console.log(a); // 10
```

`var` ignores block scope.
`let` respects block scope.

---

#  Hoisting

Hoisting means:

> Declarations are moved to the top of their scope before execution.

---

##  var Hoisting

```js
console.log(x); // undefined
var x = 10;
```

Internally behaves like:

```js
var x;
console.log(x);
x = 10;
```

---

##  let / const Hoisting

They are hoisted but not initialized.

```js
console.log(x); // X(NO) ReferenceError
let x = 10;
```

This happens because of:

---

#  Temporal Dead Zone (TDZ)

The time between:

* When variable is hoisted
* Until it is initialized

During this period → you cannot access it.

```js
{
  console.log(a); // X(NO) TDZ
  let a = 5;
}
```

TDZ prevents unsafe behavior.

---

## Why TDZ is good?

Prevents accidental usage before declaration.

---

#  Execution Context (Very Important)

JavaScript runs code inside execution contexts.

There are 2 main types:

1. Global Execution Context
2. Function Execution Context

---

##  Global Execution Context (GEC)

Created when program starts.

It has:

* Global object
* this
* Memory allocation phase
* Execution phase

---

## Two Phases

###  Memory Creation Phase

* Variables → stored as undefined
* Functions → stored fully

###  Execution Phase

* Code runs line by line
* Values assigned

---

### Example

```js
var x = 10;

function greet() {
  console.log("Hi");
}

greet();
```

Memory phase:

* x = undefined
* greet = function

Execution phase:

* x = 10
* greet() runs

---

##  Function Execution Context

Every time a function is called:

* A new execution context is created
* It has its own memory
* It has its own scope

```js
function add(a, b) {
  let result = a + b;
  return result;
}

add(2, 3);
```

When `add()` runs:

* New context created
* a = 2
* b = 3
* result stored
* returns
* context destroyed

---

#  Call Stack

JavaScript is single-threaded.

It uses a stack structure to manage execution.

LIFO (Last In First Out)

---

## Example

```js
function one() {
  two();
}

function two() {
  three();
}

function three() {
  console.log("Done");
}

one();
```

### Stack Flow

1. Global context
2. one() pushed
3. two() pushed
4. three() pushed
5. three() completes → removed
6. two() removed
7. one() removed

---

## Stack Overflow

Infinite recursion causes crash.

```js
function test() {
  test();
}

test(); // Stack overflow
```

---

#  Big Picture (Important)

When JS runs:

1. Global Execution Context created
2. Memory phase happens
3. Execution phase runs
4. Functions create new execution contexts
5. Call stack manages everything


---

#  Questions


1. Difference between block scope and function scope
2. Why `let` is safer than `var`
3. What is Temporal Dead Zone
4. What happens during execution context creation
5. How call stack works
6. Why JavaScript is single-threaded

---
