#  `let` vs `const` Behavior

Both are **block scoped** and introduced in ES6.

---

##  Block Scope

```js
{
  let a = 10;
  const b = 20;
}

console.log(a); //  ReferenceError
```

They do NOT leak outside blocks.

---

##  Reassignment

### `let` → can reassign

```js
let count = 5;
count = 10; //  allowed
```

### `const` → cannot reassign

```js
const pi = 3.14;
pi = 3.1415; //  TypeError
```

---

##  Important: Objects with const

`const` prevents reassignment, NOT mutation.

```js
const user = { name: "John" };
user.name = "Mike"; //  allowed
```

But:

```js
user = {}; //  not allowed
```

---

##  Temporal Dead Zone (TDZ)

```js
console.log(a); //  ReferenceError
let a = 5;
```

`let` and `const` are hoisted but not initialized.

---

##  Best Practice (MERN)

* Use `const` by default
* Use `let` only when value must change
* Never use `var`

---

#  Arrow Functions

Shorter function syntax with lexical `this`.

---

##  Basic Syntax

```js
const add = (a, b) => {
  return a + b;
};
```

---

##  Implicit Return

```js
const add = (a, b) => a + b;
```

---

##  Single Parameter

```js
const square = x => x * x;
```

---

##  No Parameters

```js
const greet = () => "Hello";
```

---

##  Arrow Function and `this`

Arrow functions do NOT have their own `this`.

```js
const obj = {
  name: "John",
  greet: () => {
    console.log(this.name); //  undefined
  }
};
```

Because arrow takes `this` from outer scope.

Use normal function for object methods:

```js
greet() {
  console.log(this.name);
}
```

---

#  Destructuring

Extract values from objects or arrays.

---

##  Object Destructuring

```js
const user = { name: "John", age: 25 };

const { name, age } = user;
```

---

##  Rename Variables

```js
const { name: username } = user;
```

---

##  Default Values

```js
const { city = "Unknown" } = user;
```

---

##  Array Destructuring

```js
const arr = [10, 20, 30];

const [a, b] = arr;
```

---

##  Skip Values

```js
const [first, , third] = arr;
```

---

##  Real MERN Example

```js
app.get("/users", async (req, res) => {
  const { page, limit } = req.query;
});
```

---

#  Spread & Rest Operators (`...`)

Same syntax, different purpose.

---

##  Spread (Expand)

### Arrays

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4];
```

---

### Objects

```js
const user = { name: "John" };

const updatedUser = {
  ...user,
  age: 25
};
```

Used heavily in React state updates.

---

##  Rest (Collect)

Used in parameters:

```js
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b);
}
```

---

##  Difference

Spread → expands
Rest → collects

---

#  Modules (import / export)

Used to split code into files.

---

##  Named Export

```js
// math.js
export const add = (a, b) => a + b;
```

Import:

```js
import { add } from "./math.js";
```

---

##  Default Export

```js
// user.js
export default function greet() {}
```

Import:

```js
import greet from "./user.js";
```

---

##  Multiple Named Exports

```js
export const add = () => {};
export const subtract = () => {};
```

---

##  MERN Usage

* React components
* Utility files
* Express routes
* Controllers
* Models

---

#  Optional Chaining (`?.`)

Prevents error if property does not exist.

---

Without optional chaining:

```js
console.log(user.address.city); //  error if address undefined
```

---

With optional chaining:

```js
console.log(user.address?.city);
```

Returns `undefined` instead of crashing.

---

##  Function Calls

```js
user.sayHello?.();
```

---

##  Real MERN Use

```js
const token = req.headers.authorization?.split(" ")[1];
```

---

#  Nullish Coalescing (`??`)

Provides default only if value is `null` or `undefined`.

---

##  Example

```js
const name = null;
const username = name ?? "Guest";
```

---

##  Difference from `||`

```js
const count = 0;

console.log(count || 10); // 10 
console.log(count ?? 10); // 0 
```

`||` treats 0, "", false as falsy.
`??` only checks null/undefined.

---

#  Dynamic Imports

Load modules only when needed.

Improves performance.

---

##  Syntax

```js
import("./math.js")
  .then(module => {
    console.log(module.add(2, 3));
  });
```

---

##  With async/await

```js
const module = await import("./math.js");
module.add(2, 3);
```

---

##  Why Important?

* Code splitting
* Lazy loading
* React lazy components

Example (React):

```js
const Home = React.lazy(() => import("./Home"));
```

---

#  What You Must Master for MERN

Be able to explain:

1. Why `const` is preferred
2. Why arrow functions don’t bind `this`
3. Spread vs rest difference
4. Default vs named exports
5. Why `??` is safer than `||`
6. How optional chaining prevents runtime crashes
7. Why dynamic import improves performance

---
