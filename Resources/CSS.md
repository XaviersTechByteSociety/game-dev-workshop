# CSS - Cascading Style Sheets 🎨

CSS (Cascading Style Sheets) is a styling language used to define the **look and feel** of an HTML document. By targeting HTML elements, CSS allows you to control **colors**, **fonts**, **layouts**, and **responsive design** features, bringing web pages to life.

## Core Concepts

CSS is made up of **selectors** (which choose the HTML elements to style) and **properties** (which define how those elements look). Selectors can target elements by **type**, **class**, **ID**, and more, allowing for precise control over styling.

---

## Basic CSS Properties

| Property      | Description                                          |
| ------------- | ---------------------------------------------------- |
| `color`       | Sets the text color of an element.                   |
| `background-color` | Sets the background color of an element.       |
| `font-size`   | Controls the size of the font.                       |
| `font-family` | Sets the font type (e.g., Arial, Verdana).           |
| `padding`     | Adds space inside an element's border.               |
| `margin`      | Adds space outside an element's border.              |
| `border`      | Defines the border properties (width, style, color). |
| `width`       | Sets the width of an element.                        |
| `height`      | Sets the height of an element.                       |
| `display`     | Specifies the display behavior (e.g., `block`, `inline`). |
| `position`    | Positions the element (`relative`, `absolute`, etc.). |
| `text-align`  | Aligns text within an element (left, right, center). |

---

## ✍️ Example Code

```css
/* Basic CSS styling for a web page */
body {
  background-color: #f0f0f0;
  font-family: Arial, sans-serif;
  color: #333;
}

h1 {
  color: #1a73e8;
  text-align: center;
}

p {
  font-size: 1rem;
  line-height: 1.5;
  padding: 10px;
}

button {
  background-color: #1a73e8;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
