#  Selecting Elements

##  By ID

```js
const element = document.getElementById("myId");
```

Returns single element.

---

##  By Class

```js
const elements = document.getElementsByClassName("myClass");
```

Returns HTMLCollection (array-like).

---

##  By Tag

```js
const elements = document.getElementsByTagName("p");
```

---

##  querySelector (Most Used)

Returns first matching element.

```js
const element = document.querySelector(".box");
```

---

##  querySelectorAll

Returns NodeList.

```js
const elements = document.querySelectorAll(".box");
```

You can loop:

```js
elements.forEach(el => console.log(el));
```

---

#  Creating Elements

```js
const div = document.createElement("div");
```

Add content:

```js
div.textContent = "Hello";
```

Add HTML:

```js
div.innerHTML = "<strong>Hello</strong>";
```

Append to DOM:

```js
document.body.appendChild(div);
```

---

## Insert at specific position

```js
parent.appendChild(child);          // end
parent.prepend(child);              // beginning
parent.insertBefore(newEl, refEl);  // before element
```

---

#  Modifying Elements

##  Change Text

```js
element.textContent = "New text";
```

---

##  Change HTML

```js
element.innerHTML = "<b>Bold</b>";
```

Be careful: innerHTML can cause XSS issues.

---

##  Change Attributes

```js
element.setAttribute("src", "image.png");
element.getAttribute("src");
element.removeAttribute("src");
```

---

##  Change Styles

```js
element.style.color = "red";
element.style.backgroundColor = "black";
```

---

##  Class Manipulation

```js
element.classList.add("active");
element.classList.remove("active");
element.classList.toggle("active");
element.classList.contains("active");
```

---

#  Event Listeners

Attach events to elements.

```js
button.addEventListener("click", function() {
  console.log("Button clicked");
});
```

---

## Common Events

* click
* submit
* change
* input
* mouseover
* keydown
* keyup

---

## Remove Event

```js
button.removeEventListener("click", handlerFunction);
```

---

#  Event Object

When event fires, it sends event object.

```js
button.addEventListener("click", function(event) {
  console.log(event.target);
});
```

Important properties:

* event.target
* event.type
* event.preventDefault()
* event.stopPropagation()

---

#  Event Delegation (Very Important)

Instead of adding listener to many child elements,
add one listener to parent.

Why?

* Better performance
* Works for dynamically created elements

---

## Example

```js
document.getElementById("list").addEventListener("click", function(e) {
  if (e.target.tagName === "LI") {
    console.log("Item clicked:", e.target.textContent);
  }
});
```

This works even for new `<li>` added later.

---

#  Form Handling

## Selecting Form

```js
const form = document.querySelector("form");
```

---

## Handling Submit

```js
form.addEventListener("submit", function(e) {
  e.preventDefault(); // stop page reload

  const input = document.querySelector("#name").value;
  console.log(input);
});
```

---

## Access Using Form Elements

```js
const name = form.elements["name"].value;
```

---

## Real MERN Flow

Frontend form → prevent default → collect data → send to backend using fetch.

---

#  preventDefault()

Stops default browser behavior.

Example:

* Stop form reload
* Stop link navigation

```js
e.preventDefault();
```

---

#  DOM Traversal

Moving around DOM tree.

---

##  Parent

```js
element.parentNode;
element.parentElement;
```

---

##  Children

```js
element.children;        // HTMLCollection
element.firstElementChild;
element.lastElementChild;
```

---

##  Siblings

```js
element.nextElementSibling;
element.previousElementSibling;
```

---

##  Closest (Very Useful)

```js
element.closest(".container");
```

Finds nearest ancestor matching selector.

---

#  Real Example (Mini App Logic)

```js
const form = document.querySelector("#todoForm");
const list = document.querySelector("#todoList");

form.addEventListener("submit", function(e) {
  e.preventDefault();

  const input = document.querySelector("#task");
  
  const li = document.createElement("li");
  li.textContent = input.value;

  list.appendChild(li);
  
  input.value = "";
});
```

This is how dynamic apps work without React.

---

#  What You Must Master for MERN

Even if React handles DOM:

You must understand:

* Event bubbling
* Event delegation
* DOM reflow & repaint (performance)
* How browser updates UI
* Controlled vs uncontrolled inputs (React concept)

---

#  Questionz


1. Difference between querySelector and getElementById
2. What is event bubbling?
3. What is event delegation?
4. Why use preventDefault?
5. Difference between innerHTML and textContent
6. Why direct DOM manipulation is avoided in React

---
