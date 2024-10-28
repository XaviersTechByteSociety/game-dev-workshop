# HTML - Hypertext Markup Language 🖥️

HTML (HyperText Markup Language) is the foundational language of the web. It structures the content on web pages and helps organize text, images, links, and multimedia. With HTML, you create a **framework** that CSS and JavaScript can style and manipulate to deliver a full web experience.

## Core Concepts

HTML uses **tags** (like `<p>` for paragraphs or `<a>` for links) to define content. These tags are wrapped in angle brackets and typically have an opening and closing tag. HTML also uses **attributes** within tags to add additional information.

---

## Basic HTML Tags

| Tag          | Description                                          |
| ------------ | ---------------------------------------------------- |
| `<html>`     | Wraps the entire HTML document.                      |
| `<head>`     | Contains metadata, links to CSS/JS, and page title.  |
| `<title>`    | Sets the title in the browser's title bar or tab.    |
| `<body>`     | Encloses all visible content on the page.            |
| `<h1> to <h6>` | Header tags, with `<h1>` as the largest.           |
| `<p>`        | Defines a paragraph of text.                         |
| `<a>`        | Creates hyperlinks; requires the `href` attribute.   |
| `<img>`      | Displays images; uses `src` for image URL.           |
| `<ul> / <ol>`| Unordered (bulleted) and ordered (numbered) lists.   |
| `<li>`       | List items, used within `<ul>` or `<ol>`.            |
| `<div>`      | A generic container for grouping content.            |
| `<span>`     | Inline container for styling or manipulating text.   |
| `<form>`     | Used to create forms; encloses `<input>`, `<label>`. |
| `<button>`   | Creates clickable buttons for actions or submissions.|

---

## ✍️ Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My First HTML Page</title>
</head>
<body>
  <h1>Welcome to My Website!</h1>
  <p>This is a simple web page using basic HTML tags.</p>
  <a href="https://example.com">Visit Example.com</a>
</body>
</html>
