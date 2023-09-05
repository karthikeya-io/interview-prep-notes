# 2. **DOM Manipulation**:

DOM (Document Object Model) manipulation is a fundamental aspect of client-side web development, allowing developers to interact with and modify the content of a webpage dynamically.

### 1. **Selecting & Modifying Elements**:

Before you can modify an element, you need to select it. The primary methods for this are:

- `document.getElementById('id')`: Selects an element by its ID.
- `document.querySelector('selector')`: Selects the first element that matches the provided CSS selector.
- `document.querySelectorAll('selector')`: Selects all elements that match the provided CSS selector.

Once selected, you can modify its properties.

```javascript
const title = document.getElementById("title");
title.textContent = "New Title"; // Modifying the text content
title.style.color = "red"; // Changing the color
```

### 2. **Creating Elements**:

You can create new DOM elements using the `document.createElement('tagName')` method.

```javascript
const newParagraph = document.createElement("p");
newParagraph.textContent = "This is a new paragraph!";
document.body.appendChild(newParagraph); // Appending the new element to the body
```

### 3. **Event Listeners & Event Propagation**:

Event listeners allow you to execute a function when a specific event occurs on an element.

```javascript
const button = document.querySelector("button");
button.addEventListener("click", function () {
  alert("Button was clicked!");
});
```

Event propagation consists of two phases:

- **Capture phase**: The event starts from the root and travels down to the target element.
- **Bubble phase**: The event bubbles up from the target element back to the root.

You can use the `stopPropagation` method to prevent further propagation of the event:

```javascript
button.addEventListener("click", function (event) {
  alert("Button was clicked!");
  event.stopPropagation(); // Stops the event from bubbling up or capturing down
});
```

### 4. **Form Validation**:

Form validation ensures that users fill out forms in the correct format.

```html
<form id="myForm">
  <input type="text" id="username" required />
  <button type="submit">Submit</button>
</form>
```

```javascript
const form = document.getElementById("myForm");
const username = document.getElementById("username");

form.addEventListener("submit", function (event) {
  if (username.value === "") {
    alert("Username is required!");
    event.preventDefault(); // Prevents the form from submitting
  }
});
```

### 5. **Animations & Transitions**:

Animations and transitions can be achieved using both JavaScript and CSS.

- **CSS Transitions**: Smoothly change property values over a specified duration.

```css
.box {
  width: 100px;
  height: 100px;
  background-color: red;
  transition: background-color 2s;
}

.box:hover {
  background-color: blue;
}
```

- **JavaScript Animations**: More complex animations can be achieved using the `requestAnimationFrame` method.

```javascript
let start;
function step(timestamp) {
  if (!start) start = timestamp;
  let progress = timestamp - start;
  box.style.left = Math.min(progress / 10, 200) + "px";
  if (progress < 2000) {
    requestAnimationFrame(step);
  }
}
requestAnimationFrame(step);
```

This is a simple animation that moves a box element to the right over 2 seconds.

---

DOM manipulation is a vast topic, and the above is a concise overview. Mastering these concepts is crucial for any web developer, as they form the basis for creating interactive web applications.
