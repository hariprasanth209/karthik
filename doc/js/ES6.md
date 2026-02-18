
#  1. let and const

### `let`

* Block scoped
* Can reassign
* Cannot redeclare in same scope

```js
let a = 10;
a = 20;   // ✅ allowed
```

### `const`

* Block scoped
* Cannot reassign
* Must initialize immediately

```js
const PI = 3.14;
// PI = 3; ❌ Error
```

⚠ Note: Objects declared with `const` can mutate internally.

---

#  2. Arrow Functions (`=>`)

Shorter syntax for functions.

```js
const add = (a, b) => a + b;
```

### Important Difference:

* No own `this`
* No `arguments`
* Not suitable for object methods

```js
const obj = {
  name: "Hari",
  greet: () => console.log(this.name) // ❌ undefined
};
```

---

#  3. Template Literals (`` ` ` ``)

String interpolation and multiline strings.

```js
const name = "Hari";
console.log(`Hello ${name}`);
```

Supports:

* Expression embedding
* Multiline strings

---

#  4. Default Parameters

```js
function greet(name = "Guest") {
  return `Hello ${name}`;
}
```

---

#  5. Destructuring

## Array Destructuring

```js
const arr = [1, 2, 3];
const [a, b] = arr;
```

## Object Destructuring

```js
const user = { name: "Hari", age: 22 };
const { name, age } = user;
```

### Rename while destructuring

```js
const { name: userName } = user;
```

---

#  6. Spread Operator (`...`)

Expands iterable.

## Array Copy

```js
const arr2 = [...arr1];
```

## Merge

```js
const merged = [...arr1, ...arr2];
```

## Object Copy

```js
const obj2 = { ...obj1 };
```

---

#  7. Rest Operator (`...`)

Collects remaining elements.

```js
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b);
}
```

---

#  8. Enhanced Object Literals

```js
const name = "Hari";

const user = {
  name,        // shorthand
  greet() {    // method shorthand
    return "Hello";
  }
};
```

---

#  9. Classes

Syntactic sugar over prototype-based inheritance.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hi ${this.name}`;
  }
}
```

## Inheritance

```js
class Student extends Person {
  constructor(name, grade) {
    super(name);
    this.grade = grade;
  }
}
```

---

#  10. Modules (import / export)

## Named Export

```js
export const add = () => {};
```

## Default Export

```js
export default function() {}
```

## Import

```js
import add from "./file.js";
```

---

#  11. Promises

Used for async operations.

```js
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise.then(data => console.log(data));
```

States:

* Pending
* Fulfilled
* Rejected

---

#  12. Symbol

Creates unique identifiers.

```js
const id = Symbol("id");
```

Useful for:

* Unique object keys
* Avoiding name collisions

---

#  13. Iterators & for...of

```js
const arr = [1, 2, 3];

for (const value of arr) {
  console.log(value);
}
```

Works with:

* Arrays
* Strings
* Maps
* Sets

---

#  14. Map

Key-value pairs with any data type as key.

```js
const map = new Map();
map.set("name", "Hari");
```

Methods:

* set()
* get()
* has()
* delete()
* clear()

---

#  15. Set

Stores unique values.

```js
const set = new Set([1, 2, 2, 3]);
console.log(set); // {1, 2, 3}
```

---

#  16. WeakMap & WeakSet

* Keys must be objects
* Garbage collected automatically
* Not iterable

Used for private data patterns.

---

#  17. Array Methods Added in ES6

* `find()`
* `findIndex()`
* `from()`
* `of()`

```js
Array.from("123"); // ["1","2","3"]
Array.of(1,2,3);
```

---

#  18. Object Methods Added

* `Object.assign()`
* `Object.keys()`
* `Object.values()`
* `Object.entries()`

---

#  19. String Methods Added

* `startsWith()`
* `endsWith()`
* `includes()`
* `repeat()`

---

#  20. Block Scope

Before ES6 → only function scope
After ES6 → block scope with `let` and `const`

---

#  21. Temporal Dead Zone (TDZ)

`let` and `const` cannot be accessed before declaration.

```js
console.log(a); // ❌
let a = 5;
```

---

#  22. Generators

Functions that pause execution.

```js
function* gen() {
  yield 1;
  yield 2;
}
```

---

#  23. Proxy

Intercept operations on objects.

```js
const proxy = new Proxy(target, handler);
```

Used for:

* Validation
* Logging
* Security

---

#  24. Reflect API

Works with Proxy to perform default object operations.

---

#  25. New Math Methods

* `Math.trunc()`
* `Math.sign()`
* `Math.cbrt()`

---

#  26. Number Enhancements

* `Number.isNaN()`
* `Number.isInteger()`
* `Number.parseInt()`

---

#  27. Binary & Octal Literals

```js
0b1010;  // Binary
0o755;   // Octal
```

---

#  ES6 Summary Architecture

ES6 mainly improves:

1. Scope management
2. Object-oriented structure
3. Functional programming capability
4. Asynchronous programming
5. Code readability & maintainability
