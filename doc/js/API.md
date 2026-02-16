#  localStorage & sessionStorage

Both store data in the browser.

##  Differences

| Feature  | localStorage                       | sessionStorage      |
| -------- | ---------------------------------- | ------------------- |
| Lifetime | Permanent (until manually cleared) | Until tab is closed |
| Scope    | All tabs (same origin)             | Only that tab       |
| Size     | ~5–10MB                            | ~5MB                |

Both store **only strings**.

---

##  Save Data

```js
localStorage.setItem("name", "John");
```

---

##  Get Data

```js
const name = localStorage.getItem("name");
```

---

##  Remove Data

```js
localStorage.removeItem("name");
```

---

##  Clear All

```js
localStorage.clear();
```

---

##  Storing Objects (Important)

Because storage only supports strings:

```js
const user = { name: "John", age: 25 };

localStorage.setItem("user", JSON.stringify(user));
```

Retrieve:

```js
const userData = JSON.parse(localStorage.getItem("user"));
```

---

##  Real MERN Use

Store:

* JWT token
* User preferences
* Theme settings

---

#  Fetch API (Very Important)

Used to make HTTP requests.

Modern replacement for XMLHttpRequest.

---

##  Basic GET Request

```js
fetch("https://api.example.com/users")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.log(err));
```

---

##  Using async/await (Preferred)

```js
async function getUsers() {
  try {
    const response = await fetch("https://api.example.com/users");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.log(error);
  }
}
```

---

##  POST Request

```js
fetch("https://api.example.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "John",
    age: 25
  })
});
```

---

##  Important: Check Response Status

Fetch does NOT reject on HTTP errors.

```js
const response = await fetch(url);

if (!response.ok) {
  throw new Error("Request failed");
}
```

---

##  Real MERN Flow

Frontend:

```js
const res = await fetch("/api/login", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ email, password })
});

const data = await res.json();
localStorage.setItem("token", data.token);
```

Backend verifies JWT later.

---

#  JSON Handling

JSON = JavaScript Object Notation.

Used for data exchange between client & server.

---

##  Convert Object → JSON

```js
const jsonString = JSON.stringify({ name: "John" });
```

---

##  Convert JSON → Object

```js
const obj = JSON.parse(jsonString);
```

---

##  Common Mistake

Invalid JSON:

```js
//  Wrong
{ name: "John" }
```

Valid JSON:

```js
//  Correct
{ "name": "John" }
```

Keys must be in double quotes.

---

#  URL & Query Parameters

Understanding this is essential for filtering & pagination in MERN.

---

##  Example URL

```
https://example.com/products?category=shoes&page=2
```

Query params:

* category=shoes
* page=2

---

##  Read Query Params

```js
const params = new URLSearchParams(window.location.search);

const category = params.get("category");
const page = params.get("page");
```

---

##  Add Query Params

```js
const params = new URLSearchParams();
params.append("category", "shoes");
params.append("page", 2);

const url = `https://example.com/products?${params}`;
```

---

##  Modify URL Without Reload

```js
window.history.pushState({}, "", "?page=2");
```

Used in SPAs (React Router).

---

#  Cookies (Basics)

Cookies store small data in browser and are sent to server automatically with every request.

---

##  Create Cookie

```js
document.cookie = "username=John; expires=Fri, 31 Dec 2026 12:00:00 UTC; path=/";
```

---

##  Read Cookies

```js
console.log(document.cookie);
```

Returns string of all cookies.

---

##  Delete Cookie

Set expiration to past:

```js
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
```

---

##  Cookies vs localStorage

| Feature                      | Cookies | localStorage |
| ---------------------------- | ------- | ------------ |
| Sent to server automatically | Yes     | No           |
| Size                         | ~4KB    | ~5MB         |
| Expiration control           | Yes     | Manual       |
| Secure flag                  | Yes     | No           |

---

##  In Real MERN Authentication

Two common approaches:

###  JWT in localStorage

* Easy
* Vulnerable to XSS

###  HTTP-only Cookies (Better Security)

* Cannot be accessed by JS
* Safer against XSS
* Used in production apps

---

#  What You Must Master for MERN

You must clearly understand:

1. How fetch works internally
2. Difference between localStorage and cookies
3. Why HTTP-only cookies are safer
4. Why fetch does not reject on 404
5. How to send authorization headers

Example:

```js
fetch("/api/profile", {
  headers: {
    Authorization: `Bearer ${token}`
  }
});
```

---
