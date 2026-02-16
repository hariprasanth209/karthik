#  Synchronous vs Asynchronous

##  Synchronous

Code runs line by line.
Each task must finish before the next starts.

```js
console.log("Start");
console.log("Middle");
console.log("End");
```

Output:

```
Start
Middle
End
```

Blocking behavior.

---

##  Asynchronous

Some tasks run in background without blocking the main thread.

Example:

* API calls
* Database queries
* File reading
* Timers

```js
console.log("Start");

setTimeout(() => {
  console.log("Middle");
}, 2000);

console.log("End");
```

Output:

```
Start
End
Middle
```

JavaScript is single-threaded but can handle async using the Event Loop.

---

#  setTimeout & setInterval

##  setTimeout

Runs once after delay.

```js
setTimeout(() => {
  console.log("Runs after 2 seconds");
}, 2000);
```

---

##  setInterval

Runs repeatedly.

```js
setInterval(() => {
  console.log("Runs every 1 second");
}, 1000);
```

Stop it using:

```js
const id = setInterval(() => {}, 1000);
clearInterval(id);
```

---

#  Callback Pattern

A callback is a function passed to another function and executed later.

---

## Basic Example

```js
function fetchData(callback) {
  setTimeout(() => {
    callback("Data received");
  }, 1000);
}

fetchData(function(result) {
  console.log(result);
});
```

---

## Problem: Callback Hell

Nested callbacks become messy.

```js
getUser(function(user) {
  getOrders(user.id, function(orders) {
    getPayment(orders[0], function(payment) {
      console.log(payment);
    });
  });
});
```

Hard to read. Hard to debug.

This is why Promises were introduced.

---

#  Promises

A Promise represents a value that will be available in the future.

States:

* Pending
* Fulfilled
* Rejected

---

## Creating a Promise

```js
const promise = new Promise((resolve, reject) => {
  let success = true;

  if (success) {
    resolve("Success");
  } else {
    reject("Failed");
  }
});
```

---

## Consuming a Promise

```js
promise
  .then(result => console.log(result))
  .catch(error => console.log(error));
```

---

#  Promise Chaining

Avoid nested callbacks by chaining.

```js
fetchUser()
  .then(user => fetchOrders(user.id))
  .then(orders => fetchPayment(orders[0]))
  .then(payment => console.log(payment))
  .catch(error => console.log(error));
```

Cleaner than callback hell.

Each `.then()` returns a new promise.

---

#  async / await (Modern Standard)

Cleaner way to handle promises.

---

## Example

```js
async function getData() {
  const result = await fetch("https://api.com/data");
  const data = await result.json();
  console.log(data);
}
```

`await` pauses execution until promise resolves.

Only works inside `async` function.

---

## Behind the scenes

`async/await` is syntactic sugar over promises.

---

#  Error Handling with try/catch

With async/await:

```js
async function getData() {
  try {
    const result = await fetch("wrong-url");
    const data = await result.json();
    console.log(data);
  } catch (error) {
    console.log("Error:", error);
  }
}
```

---

With promises:

```js
fetchData()
  .then(data => console.log(data))
  .catch(error => console.log(error));
```

---

#  Promise.all

Runs multiple promises in parallel.

---

## Example

```js
Promise.all([
  fetchUser(),
  fetchOrders(),
  fetchPayments()
])
.then(results => {
  console.log(results);
})
.catch(error => {
  console.log(error);
});
```

---

Important:

* If one fails → entire Promise.all fails
* Executes in parallel (faster)

---

#  Event Loop (Deep Understanding)

This is the core engine.

JavaScript has:

1. Call Stack
2. Web APIs
3. Callback Queue
4. Event Loop

---

## How It Works

Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
```

Output:

```
Start
End
Timeout
```

---

## Why?

Step-by-step:

1. "Start" → pushed to call stack → executed
2. setTimeout → registered in Web API
3. "End" → executed
4. Timer finishes → callback goes to callback queue
5. Event loop checks:

   * Is call stack empty?
   * Yes → push callback to stack
6. "Timeout" runs

---

## Microtasks vs Macrotasks

Microtasks:

* Promise `.then`
* queueMicrotask

Macrotasks:

* setTimeout
* setInterval

---

## Example

```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

Output:

```
Start
End
Promise
Timeout
```

Why?

Microtasks (Promises) run before macrotasks (setTimeout).

---

#  Real MERN Importance

You must understand this because:

* Express routes are async
* MongoDB queries return promises
* React API calls use async/await
* JWT verification is async
* File uploads are async
* Node is non-blocking

---

#  Common Backend Pattern

```js
app.get("/users", async (req, res) => {
  try {
    const users = await User.find();
    res.json(users);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});
```

This is real MERN code.

---

#  Interview-Level Understanding

You must clearly explain:

1. Why JavaScript is non-blocking
2. What the event loop does
3. Difference between callback queue and call stack
4. Why Promise runs before setTimeout
5. Difference between async/await and then/catch
6. When to use Promise.all

---
