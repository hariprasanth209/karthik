#  Prototype Chain

## Core Idea

Every object in JavaScript has a hidden property:

```
[[Prototype]]
```

Accessible via:

```js
Object.getPrototypeOf(obj)
```

Or:

```js
obj.__proto__
```

---

## Example

```js
const user = {
  name: "Hari"
};

console.log(user.toString());
```

Why does `toString()` work?

Because:

```
user → Object.prototype → null
```

JavaScript looks up the prototype chain when a property is not found.

This is called the **prototype chain lookup**.

---

## How It Works

If you access:

```js
user.age
```

JS checks:

1. Does `user` have `age`?
2. If not → check its prototype
3. Continue until null

---

#  Constructor Functions

Before ES6 classes, this was how OOP was done.

---

## Example

```js
function User(name, age) {
  this.name = name;
  this.age = age;
}
```

Create object using `new`:

```js
const u1 = new User("Hari", 22);
```

---

## What `new` Does Internally

When you write:

```js
new User()
```

JavaScript:

1. Creates empty object {}
2. Links it to User.prototype
3. Sets `this` to new object
4. Returns the object

---

# Adding Methods (Correct Way)

Instead of:

```js
function User(name) {
  this.name = name;
  this.greet = function() {
    console.log("Hi");
  };
}
```

Better:

```js
User.prototype.greet = function() {
  console.log("Hi " + this.name);
};
```

Why?

Because method is shared across instances.

Memory efficient.

---

#  ES6 Classes

Cleaner syntax over prototypes.

---

## Example

```js
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log("Hi " + this.name);
  }
}
```

Create instance:

```js
const u1 = new User("Hari", 22);
u1.greet();
```

Internally → still uses prototype.

---

#  Inheritance

Allows one class to inherit properties/methods from another.

---

## Constructor Function Inheritance

Old style (complex and less used now).

---

## ES6 Inheritance (Preferred)

```js
class Admin extends User {
  constructor(name, age, role) {
    super(name, age);   // calls parent constructor
    this.role = role;
  }

  deleteUser() {
    console.log("User deleted");
  }
}
```

---

## Example Usage

```js
const admin = new Admin("Hari", 22, "superadmin");
admin.greet();        // inherited
admin.deleteUser();   // own method
```

---

## Prototype Chain Now Looks Like

```
admin → Admin.prototype → User.prototype → Object.prototype → null
```

---

#  Static Methods

Static methods belong to the class, not instances.

---

## Example

```js
class MathUtil {
  static add(a, b) {
    return a + b;
  }
}
```

Call like:

```js
MathUtil.add(5, 3);
```

Not:

```js
new MathUtil().add(); X(NO)
```

---

## Real MERN Use

Utility helpers
Validation classes
Factory methods

---

#  Encapsulation

Encapsulation means:

> Hiding internal implementation details and exposing only necessary functionality.

---

## Basic Encapsulation (Using Closure)

```js
function BankAccount(balance) {
  let _balance = balance;

  this.deposit = function(amount) {
    _balance += amount;
  };

  this.getBalance = function() {
    return _balance;
  };
}
```

`_balance` is private.

---

## Modern Private Fields (ES2022)

```js
class BankAccount {
  #balance;

  constructor(balance) {
    this.#balance = balance;
  }

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}
```

Now:

```js
account.#balance; X(NO) Error
```

---

#  Real MERN Context

OOP in MERN is used for:

* Model classes
* Service layers
* Utility classes
* Authentication managers
* DTO patterns

However:
Most modern MERN uses **functional programming style** more than classical OOP.

Still, understanding prototypes is essential.

---

# Important Differences

| Feature        | Constructor Function | ES6 Class |
| -------------- | -------------------- | --------- |
| Syntax         | Old                  | Modern    |
| Under the hood | Prototype            | Prototype |
| Readability    | Lower                | Higher    |

---

#  Things You Must Clearly Understand

1. What is prototype chain?
2. How does property lookup work?
3. What does `new` do internally?
4. Why put methods on prototype?
5. Difference between static & instance methods?
6. How inheritance works with `extends`?
7. What is encapsulation in JS?

---

#  Important Reality

In MERN:

* React → mostly functional components
* Node/Express → mostly functional style
* But understanding OOP helps in large-scale architecture

---
