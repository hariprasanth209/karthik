
---

#  if / else

Used for conditional branching.

## Basic Syntax

```js
if (condition) {
  // runs if condition is true
}
```

---

## if / else

```js
let age = 20;

if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Minor");
}
```

---

## else if ladder

```js
let marks = 75;

if (marks >= 90) {
  console.log("A");
} else if (marks >= 70) {
  console.log("B");
} else if (marks >= 50) {
  console.log("C");
} else {
  console.log("Fail");
}
```

---

## Important Concepts

###  Condition must evaluate to Boolean

```js
if ("hello") {   // truthy
  console.log("Runs");
}
```

Falsy values:

```
false, 0, "", null, undefined, NaN
```

---

## Nested if

```js
let isLoggedIn = true;
let isAdmin = true;

if (isLoggedIn) {
  if (isAdmin) {
    console.log("Access granted");
  }
}
```

---

#  switch

Used when checking multiple values of same variable.

## Syntax

```js
switch (expression) {
  case value1:
    // code
    break;

  case value2:
    // code
    break;

  default:
    // fallback
}
```

---

## Example

```js
let role = "admin";

switch (role) {
  case "admin":
    console.log("Full access");
    break;

  case "user":
    console.log("Limited access");
    break;

  default:
    console.log("No access");
}
```

---

## Important: break

Without break → fall-through happens.

```js
let x = 1;

switch (x) {
  case 1:
    console.log("One");
  case 2:
    console.log("Two");
}
```

Output:

```
One
Two
```

Because no `break`.

---

## When to use switch?

* Clean handling of fixed values
* Role handling
* API action types
* Menu systems

---

#  Loops

Used for repetition.

---

#  for Loop (Most Used)

## Syntax

```js
for (initialization; condition; increment) {
  // code
}
```

---

## Example

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

Output:

```
0 1 2 3 4
```

---

## Reverse loop

```js
for (let i = 5; i > 0; i--) {
  console.log(i);
}
```

---

## Loop through array

```js
let arr = [10, 20, 30];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

---

#  while Loop

Runs while condition is true.

```js
let i = 0;

while (i < 5) {
  console.log(i);
  i++;
}
```

Use when:

* You don’t know number of iterations beforehand.

---

#  do-while Loop

Runs at least once.

```js
let i = 0;

do {
  console.log(i);
  i++;
} while (i < 5);
```

Even if condition is false initially → runs once.

---

#  for...of

Used to iterate over iterable values (arrays, strings).

## Example: Array

```js
let arr = [10, 20, 30];

for (let value of arr) {
  console.log(value);
}
```

Output:

```
10
20
30
```

---

## Example: String

```js
let name = "Sam";

for (let ch of name) {
  console.log(ch);
}
```

---

## When to use?

* Clean array iteration
* No need for index
* Preferred over traditional for in modern JS

---

#  for...in

Used to iterate over object keys.

## Example: Object

```js
let user = {
  name: "Sam",
  age: 27
};

for (let key in user) {
  console.log(key);         // name, age
  console.log(user[key]);   // Sam, 27
}
```

---

## Important Difference

| Loop Type | Used For         |
| --------- | ---------------- |
| for       | Full control     |
| for...of  | Values of arrays |
| for...in  | Object keys      |

---

##  Don’t use for...in for arrays

Because it iterates over keys (indexes as strings).

---

#  break & continue

---

##  break

Stops the loop immediately.

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break;
  }
  console.log(i);
}
```

Output:

```
0 1 2 3 4
```

---

##  continue

Skips current iteration.

```js
for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue;
  }
  console.log(i);
}
```

Output:

```
0 1 3 4
```

---

#  Real MERN Usage Examples

### Backend validation:

```js
if (!email) {
  return res.status(400).json({ error: "Email required" });
}
```

### Loop through DB results:

```js
for (let user of users) {
  console.log(user.name);
}
```

### Role-based control:

```js
switch (user.role) {
  case "admin":
    // admin logic
    break;
}
```

---

# Questions

1. Difference between for and while
2. Difference between for...of and for...in
3. Why break is important in switch
4. When do-while is useful
5. Truthy/falsy in if conditions

---
