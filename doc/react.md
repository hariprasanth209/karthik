 **two components sharing login state globally**.

In React, the correct way to share state globally between components is **Context API**.

build this structure:

```
App
 ├── LoginButton
 └── Dashboard
```

Both components will access the same `isLoggedIn` state.

---

#  Step 1 — Create Global Context

###  `AuthContext.jsx`

```jsx
import { createContext, useState } from "react";

export const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <AuthContext.Provider value={{ isLoggedIn, setIsLoggedIn }}>
      {children}
    </AuthContext.Provider>
  );
}
```

### What this does:

* Creates a global context
* Stores login state
* Makes it available to all child components

---

#  Step 2 — Wrap App with Provider

###  `main.jsx`

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AuthProvider } from "./AuthContext";

ReactDOM.createRoot(document.getElementById("root")).render(
  <AuthProvider>
    <App />
  </AuthProvider>
);
```

Now the entire app can access login state.

---

#  Step 3 — Login Button Component

###  `LoginButton.jsx`

```jsx
import { useContext } from "react";
import { AuthContext } from "./AuthContext";

function LoginButton() {
  const { isLoggedIn, setIsLoggedIn } = useContext(AuthContext);

  return (
    <button onClick={() => setIsLoggedIn(!isLoggedIn)}>
      {isLoggedIn ? "Logout" : "Login"}
    </button>
  );
}

export default LoginButton;
```

---

#  Step 4 — Dashboard Component

###  `Dashboard.jsx`

```jsx
import { useContext } from "react";
import { AuthContext } from "./AuthContext";

function Dashboard() {
  const { isLoggedIn } = useContext(AuthContext);

  return (
    <div>
      <h2>
        {isLoggedIn ? "Welcome to Dashboard" : "Please Login First"}
      </h2>
    </div>
  );
}

export default Dashboard;
```

---

#  Step 5 — Use Both in App

###  `App.jsx`

```jsx
import LoginButton from "./LoginButton";
import Dashboard from "./Dashboard";

function App() {
  return (
    <div>
      <h1>Global Login Example</h1>
      <LoginButton />
      <Dashboard />
    </div>
  );
}

export default App;
```

---

#  Output Behavior

### Initially:

```
Global Login Example
[Login]
Please Login First
```

### After clicking Login:

```
[Logout]
Welcome to Dashboard
```

Both components update automatically because they share the same global state.

---

#  What Just Happened?

* `useState` is inside `AuthProvider`
* `AuthContext` makes it globally accessible
* `useContext` allows components to consume it
* When `setIsLoggedIn` updates state → both components re-render

---


