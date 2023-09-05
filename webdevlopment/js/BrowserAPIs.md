## 3. **Browser APIs**:

Browser APIs (Application Programming Interfaces) provide a set of functionalities that allow developers to interact with the browser and perform various tasks that aren't directly related to the DOM or JavaScript language itself.

### 1. **Fetch API / XMLHttpRequest**:

Both of these are used to make HTTP requests to retrieve or send data to/from a server.

- **XMLHttpRequest**:

This is the older method of making asynchronous requests.

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "https://api.example.com/data", true);
xhr.onload = function () {
  if (xhr.status >= 200 && xhr.status < 400) {
    const data = JSON.parse(xhr.responseText);
    console.log(data);
  } else {
    console.error("Server returned an error");
  }
};
xhr.onerror = function () {
  console.error("Request failed");
};
xhr.send();
```

- **Fetch API**:

A modern way to make asynchronous requests. It returns promises and is generally more powerful and flexible than `XMLHttpRequest`.

`fetch()` is a modern JavaScript function used for making network requests, typically to fetch resources from a server or API. It's a part of the Web API provided by web browsers and is widely used for performing HTTP requests asynchronously. `fetch()` returns a Promise that resolves to the Response object representing the response to the request. You can then use methods like `.json()` to parse the response or handle it in other ways.

Here's an explanation of `fetch()` with examples:

1. **Basic GET Request**:

   ```javascript
   // Making a GET request to a JSON API
   fetch("https://jsonplaceholder.typicode.com/posts/1")
     .then((response) => response.json())
     .then((data) => console.log(data))
     .catch((error) => console.error("Error:", error));
   ```

   In this example, we fetch data from a JSON API, and once the response is received, we parse it as JSON using `.json()`. The data is logged to the console.

2. **POST Request with JSON Payload**:

   ```javascript
   // Making a POST request with JSON data
   const postData = {
     title: "Hello",
     body: "World",
     userId: 1,
   };

   fetch("https://jsonplaceholder.typicode.com/posts", {
     method: "POST",
     headers: {
       "Content-Type": "application/json",
     },
     body: JSON.stringify(postData),
   })
     .then((response) => response.json())
     .then((data) => console.log(data))
     .catch((error) => console.error("Error:", error));
   ```

   In this example, we make a POST request to an API with JSON data in the request body. We specify the HTTP method, headers, and stringify the JSON data using `JSON.stringify()`.

3. **Handling Errors**:

   ```javascript
   fetch("https://jsonplaceholder.typicode.com/nonexistent", {
     method: "GET",
   })
     .then((response) => {
       if (!response.ok) {
         throw new Error("Network response was not ok");
       }
       return response.json();
     })
     .then((data) => console.log(data))
     .catch((error) => console.error("Error:", error));
   ```

   Here, we check for errors in the response using `response.ok`. If the response is not okay (e.g., a 404 status), we throw an error. This allows us to handle network errors gracefully.

4. **Handling Headers**:

   ```javascript
   fetch("https://jsonplaceholder.typicode.com/posts/1")
     .then((response) => {
       // Accessing response headers
       const contentType = response.headers.get("content-type");
       console.log(`Content-Type: ${contentType}`);
       return response.json();
     })
     .then((data) => console.log(data))
     .catch((error) => console.error("Error:", error));
   ```

   You can access response headers using `response.headers.get('header-name')`. In this example, we log the Content-Type header.

`fetch()` is a versatile and powerful tool for making network requests in JavaScript. It's supported in most modern browsers and provides a clean and promise-based API for handling HTTP requests and responses.

### 2. **LocalStorage & SessionStorage**:

These are web storage solutions that allow you to store key-value pairs in a web browser.

- **LocalStorage**: Data stored here persists even after the browser is closed.

```javascript
localStorage.setItem("name", "John");
console.log(localStorage.getItem("name")); // Outputs: John
localStorage.removeItem("name");
```

- **SessionStorage**: Data stored here gets cleared when the page's session ends (i.e., when the tab is closed).

```javascript
sessionStorage.setItem("sessionKey", "12345");
console.log(sessionStorage.getItem("sessionKey")); // Outputs: 12345
sessionStorage.removeItem("sessionKey");
```

### 3. **Geolocation API**:

This allows you to get the geographical position of a user.

```javascript
if ("geolocation" in navigator) {
  navigator.geolocation.getCurrentPosition(function (position) {
    console.log("Latitude:", position.coords.latitude);
    console.log("Longitude:", position.coords.longitude);
  });
} else {
  console.log("Geolocation is not supported by this browser.");
}
```

### 4. **File API**:

This provides the ability to read the contents of files the user selects, as well as to create new files and save them to the user's system.

For example, reading a selected file:

```javascript
const fileInput = document.querySelector('input[type="file"]');

fileInput.addEventListener("change", function (event) {
  const file = event.target.files[0];
  const reader = new FileReader();

  reader.onload = function (e) {
    console.log(e.target.result); // This will print the file's content
  };

  reader.readAsText(file);
});
```

### 5. **WebSockets**:

WebSockets provide a full-duplex communication channel over a single, long-lived connection. It's useful for real-time applications like chat apps, online gaming, and live sports updates.

```javascript
const socket = new WebSocket("ws://example.com/socketserver");

socket.onopen = function (event) {
  socket.send("Hello Server!");
};

socket.onmessage = function (event) {
  console.log("Received:", event.data);
};

socket.onclose = function (event) {
  if (event.wasClean) {
    console.log(
      `Connection closed cleanly, code=${event.code}, reason=${event.reason}`
    );
  } else {
    console.error("Connection died");
  }
};

socket.onerror = function (error) {
  console.error(`[error] ${error.message}`);
};
```

---

These browser APIs significantly expand the capabilities of web applications, allowing for a wide range of functionalities and more dynamic, interactive, and responsive user experiences.
