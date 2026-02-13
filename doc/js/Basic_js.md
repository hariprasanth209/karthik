#  JS BASIC
---

#  Variables (`var`, `let`, `const`)

##  What is a Variable?

A variable stores a value in memory.

```js
let name = "Sam";
```

---

##  var (OLD – avoid in modern JS)

```js
var x = 10;
```

### Problems:

* Function scoped (not block scoped)
* Hoisted (can be accessed before declaration as `undefined`)
* Can be redeclared

```js
var a = 5;
var a = 10;   // Allowed X(NO) (bad practice)
```

```js
if (true) {
  var b = 20;
}
console.log(b); // 20 (leaks outside block)
```

---

##  let (Modern – use this)

```js
let age = 25;
```

### Features:

* Block scoped
* Cannot redeclare in same scope
* Hoisted but in Temporal Dead Zone

```js
let x = 10;
let x = 20;  // X(NO) Error
```

```js
if (true) {
  let y = 30;
}
console.log(y); // X(NO) Error
```

---

##  const (Use by default)

```js
const pi = 3.14;
```

### Rules:

* Block scoped
* Cannot reassign
* Must initialize immediately

```js
const x; // X(NO) Error
```

```js
const a = 10;
a = 20;  // X(NO) Error
```

### Important:

For objects/arrays → you cannot reassign, but you can modify inside.

```js
const user = { name: "Sam" };
user.name = "Atman"; //  allowed
```

---

###  Best Practice

* Use `const` by default
* Use `let` when value changes
* Never use `var`

---

# Data Types (Primitive vs Reference)

JavaScript has **dynamic typing**.

```js
let x = 10;
x = "Hello";  // Allowed
```

---

##  Primitive Types (Stored by Value)

1. String
2. Number
3. Boolean
4. Undefined
5. Null
6. BigInt
7. Symbol

Example:

```js
let name = "Sam";      // String
let age = 25;           // Number
let isStudent = true;   // Boolean
let x;                  // Undefined
let y = null;           // Null
```

### Copy behavior:

```js
let a = 10;
let b = a;
b = 20;

console.log(a); // 10 (unchanged)
```

---

##  Reference Types (Stored by Reference)

1. Object
2. Array
3. Function

```js
let user = { name: "Sam" };
let arr = [1, 2, 3];
```

### Copy behavior:

```js
let obj1 = { name: "Sam" };
let obj2 = obj1;

obj2.name = "Atman";

console.log(obj1.name); // "Atman"
```

Because both point to same memory.

---

# Type Coercion

JavaScript automatically converts types.

---

##  Implicit Coercion

```js
"5" + 2      // "52"
"5" - 2      // 3
true + 1     // 2
false + 1    // 1
```

`+` prefers string
`-`, `*`, `/` prefer number

---

##  Explicit Coercion

```js
Number("10")    // 10
String(100)     // "100"
Boolean(1)      // true
```

---

##  Truthy & Falsy

Falsy values:

* false
* 0
* ""
* null
* undefined
* NaN

Everything else = truthy

```js
if ("hello") {
  console.log("Runs");
}
```

---

##  == vs ===

```js
5 == "5"   // true (coercion happens)
5 === "5"  // false (strict check)
```

Always use:

```
===
```

---

# Operators

---

##  Arithmetic

```js
+  -  *  /  %  **
```

---

##  Comparison

```js
> < >= <=
== !=
=== !==
```

---

##  Logical

```js
&&   // AND
||   // OR
!    // NOT
```

Example:

```js
true && false   // false
true || false   // true
```

---

##  Assignment

```js
= 
+= 
-= 
*= 
/= 
```

---

##  Ternary Operator

```js
let result = age > 18 ? "Adult" : "Minor";
```

---

##  Nullish Coalescing (Modern)

Returns right side only if left is null or undefined

```js
let name = null;
let result = name ?? "Guest";
```

---

# Template Literals

Used with backticks `` ` ``

```js
let name = "Sam";
let age = 27;

console.log(`My name is ${name} and I am ${age} years old.`);
```

---

## Multi-line strings

```js
let text = `
Hello
World
`;
```

---

## Expression inside template

```js
console.log(`2 + 2 = ${2 + 2}`);
```

---

#  Strict Mode

Enables safer JavaScript.

```js
"use strict";
```

---

## Why use strict mode?

1. Prevents accidental globals
2. Disallows duplicate parameters
3. Makes errors visible
4. Blocks silent failures

Example:

```js
"use strict";

x = 10; // X(NO) Error (without declaration)
```

Without strict → JS creates global variable automatically (dangerous).

---

#  Real MERN Insight

In Node.js and modern React:

* Strict mode is enabled automatically in modules
* Always use `const` / `let`
* Always use `===`
* Avoid implicit coercion confusion

---

#  You Must Be Able To Answer

1. Why `let` is better than `var`
2. Difference between primitive & reference
3. What is type coercion
4. Difference between `==` and `===`
5. Why strict mode matters

---
---

