# JavaScript - Making the Web Interactive ⚡

JavaScript is a powerful programming language that adds **interactivity** to web pages. While HTML structures the content and CSS styles it, JavaScript manipulates it dynamically—responding to events, validating forms, creating animations, and more.

## Core Concepts

JavaScript is event-driven, meaning it can execute code in response to user interactions. It uses **variables** to store data, **functions** to perform actions, and **events** to react to actions like clicks or keyboard inputs.

---

## Basic JavaScript Concepts

| Concept           | Description                                          |
| ----------------- | ---------------------------------------------------- |
| `variables`       | Store data values (e.g., `let`, `const`).            |
| `functions`       | Define reusable blocks of code.                      |
| `conditionals`    | Execute code based on conditions (`if`, `else`).     |
| `loops`           | Repeat code blocks (`for`, `while`).                 |
| `arrays`          | Store multiple values in a single variable.          |
| `objects`         | Group related data and functions.                    |
| `DOM Manipulation`| Access and change HTML elements with JavaScript.     |
| `events`          | Trigger code with user interactions (click, hover).  |

---

## ✍️ Example Code

```javascript
// Basic JavaScript example for a button click event
let button = document.getElementById("myButton");

button.addEventListener("click", function() {
  alert("Button was clicked!");
});

// Adding two numbers
function add(a, b) {
  return a + b;
}

console.log(add(5, 3)); // Outputs 8
