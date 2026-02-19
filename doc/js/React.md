
---

#  What is a Component in React?

In React, **everything is a component**.

A component is a **function that returns UI (JSX)**.

### Basic Functional Component

```jsx
function Header() {
  return <h1>Hello World</h1>;
}
```

Modern syntax (recommended):

```jsx
const Header = () => {
  return <h1>Hello World</h1>;
};
```

Then use it like:

```jsx
<Header />
```

### Types of Components

| Type       | Description                          |
| ---------- | ------------------------------------ |
| Functional | Normal JS function (modern standard) |
| Class      | Old way (rarely used now)            |

You should focus only on **functional components**.

---

#  What is JSX?

JSX = **JavaScript XML**

It looks like HTML, but it is NOT HTML.

Example:

```jsx
const element = <h1>Hello</h1>;
```

Behind the scenes, React converts it to:

```js
React.createElement("h1", null, "Hello");
```

### JSX Rules (Very Important)

#### ✅ 1. Must return single parent

❌ Wrong:

```jsx
return (
  <h1>Hello</h1>
  <p>World</p>
);
```

✅ Correct:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);
```

---

#### ✅ 2. class → className

```jsx
<div className="box"></div>
```

---

#### ✅ 3. Use {} for JavaScript

```jsx
const name = "Hari";

return <h1>{name}</h1>;
```

You can write:

```jsx
<h1>{2 + 2}</h1>
<h1>{isLoggedIn ? "Yes" : "No"}</h1>
```

---

#  Props (Very Important Concept)

Props = **Data passed from Parent → Child**

Think of props like function parameters.

---

## Basic Example

### Parent Component

```jsx
function App() {
  return <User name="Hari" age={21} />;
}
```

### Child Component

```jsx
const User = (props) => {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>{props.age}</p>
    </div>
  );
};
```

---

## Better Way (Destructuring)

```jsx
const User = ({ name, age }) => {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
    </div>
  );
};
```

---

## Props Rules

* Props are **read-only**
* Child cannot modify props
* Data flows **one direction** (Parent → Child)

This is called:

> **Unidirectional Data Flow**

---

## Passing Functions as Props

Very important in real projects.

```jsx
function App() {
  const handleClick = () => {
    alert("Clicked");
  };

  return <Button onClick={handleClick} />;
}
```

Child:

```jsx
const Button = ({ onClick }) => {
  return <button onClick={onClick}>Click Me</button>;
};
```

This allows **child → parent communication**.

---

#  Component Types in Real Projects

In real-world apps, components are categorized:

### 1. Presentational (UI)

Only UI.

Example:

```jsx
Card.jsx
Button.jsx
Navbar.jsx
```

---

### 2. Container / Smart Components

Handles:

* API calls
* State
* Business logic

Example:

```jsx
UserList.jsx
Dashboard.jsx
```

---

#  React Project Structure (Professional Level)

When you create a project using Vite or Create React App:

### Basic Structure

```
my-app/
│
├── public/
│   └── index.html
│
├── src/
│   ├── assets/
│   ├── components/
│   ├── pages/
│   ├── hooks/
│   ├── context/
│   ├── services/
│   ├── App.jsx
│   └── main.jsx
│
└── package.json
```

---

##  public/

Static files:

* index.html
* images

---

##  src/

Main development folder.

---

###  components/

Reusable UI components.

```
components/
  Button.jsx
  Card.jsx
  Navbar.jsx
```

---

###  pages/

Page-level components.

```
pages/
  Home.jsx
  About.jsx
  Login.jsx
```

These are connected to routing.

---

###  hooks/

Custom hooks.

```
hooks/
  useFetch.js
  useAuth.js
```

---

###  services/

API logic.

```
services/
  api.js
  userService.js
```

---

###  context/

Global state using React Context.

```
context/
  AuthContext.jsx
```

---

#  How Rendering Works (Important)

In React:

1. Component runs
2. Returns JSX
3. React creates Virtual DOM
4. Compares with previous DOM (Diffing)
5. Updates only changed parts

This makes it fast.

---

#  Real Example (Mini Project Structure)

### App.jsx

```jsx
import Navbar from "./components/Navbar";
import Home from "./pages/Home";

function App() {
  return (
    <>
      <Navbar />
      <Home />
    </>
  );
}

export default App;
```

---

### components/Navbar.jsx

```jsx
const Navbar = () => {
  return <h1>My Website</h1>;
};

export default Navbar;
```

---

### pages/Home.jsx

```jsx
const Home = () => {
  return <p>Welcome to homepage</p>;
};

export default Home;
```

---
