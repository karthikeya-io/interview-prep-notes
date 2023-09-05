# JavaScript fundamentals.

## Basics

### 1. **Syntax & Basics**:

JavaScript is a case-sensitive language with a C-style syntax. It uses curly braces `{}` to define blocks of code and semicolons `;` to end statements (though they're often optional due to Automatic Semicolon Insertion).

```javascript
console.log("Hello, World!");
```

### 2. **Variables (let, const)**:

- **let**: Allows you to declare block-level variables. The value of these variables can be changed.

```javascript
let name = "John";
name = "Doe"; // This is valid
```

- **const**: Allows you to declare variables whose value cannot be reassigned. It's good for values that you want to remain constant throughout your code.

```javascript
const PI = 3.14159;
PI = 3.14; // This will throw an error
```

### 3. **Data Types**:

- **Number**: Represents both integers and floats.

```javascript
let age = 25; // integer
let average = 5.5; // float
```

- **String**: Represents a sequence of characters.

```javascript
let greeting = "Hello, World!";
let anotherGreeting = "Hello again!";
```

- **Boolean**: Represents a true or false value.

```javascript
let isOnline = true;
let isOffline = false;
```

- **Null**: Represents a non-value or no value.

```javascript
let emptyValue = null;
```

- **Undefined**: Represents a variable that has been declared but hasn't been assigned a value.

```javascript
let notDefined;
console.log(notDefined); // Outputs: undefined
```

- **Symbol**: Represents a unique and immutable data type and is often used as an identifier for object properties.

```javascript
const uniqueSymbol = Symbol("description");
```

- **BigInt**: Represents large integers that cannot be represented by the Number type.

```javascript
const bigNumber = 1234567890123456789012345678901234567890n;
```

### 4. **Operators**:

- Arithmetic Operators: `+`, `-`, `*`, `/`, `%`, `++`, `--`

```javascript
let x = 5 + 10; // 15
```

- Comparison Operators: `==`, `===`, `!=`, `!==`, `<`, `>`, `<=`, `>=`

```javascript
if (5 === "5") {
  // false because of type mismatch
  // This block won't execute
}
```

- Logical Operators: `&&`, `||`, `!`

```javascript
let result = true && false; // false
```

### 5. **Conditional Statements**:

- **if, else**:

```javascript
if (age > 18) {
  console.log("You are an adult.");
} else {
  console.log("You are a minor.");
}
```

- **switch**:

```javascript
switch (day) {
  case "Monday":
    console.log("Start of the work week.");
    break;
  case "Friday":
    console.log("Almost the weekend!");
    break;
  default:
    console.log("It's a regular day.");
}
```

### 6. **Loops**:

- **for**:

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

- **while**:

```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

- **do-while**:

```javascript
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

- **for-of** (Iterates over iterable objects like arrays, strings):

```javascript
let colors = ["red", "green", "blue"];
for (let color of colors) {
  console.log(color);
}
```

- **for-in** (Iterates over the properties of an object):

```javascript
let person = { name: "John", age: 30 };
for (let key in person) {
  console.log(key, person[key]);
}
```

## Functions

### 1. **Function Declarations & Expressions**:

- **Function Declaration**: This is the most common way to define a function. The function can be called before its definition due to hoisting.

```javascript
function greet(name) {
  return "Hello, " + name + "!";
}
console.log(greet("Alice")); // Outputs: Hello, Alice!
```

- **Function Expression**: Here, a function is assigned to a variable. It cannot be called before its definition.

```javascript
const greet = function (name) {
  return "Hello, " + name + "!";
};
console.log(greet("Bob")); // Outputs: Hello, Bob!
```

### 2. **Arrow Functions**:

Introduced in ES6, arrow functions provide a more concise syntax for writing functions. They also have a lexical `this`, meaning they don't create their own `this` context.

```javascript
const greet = (name) => {
  return "Hello, " + name + "!";
};
// Even shorter for single parameter and single statement functions
const square = (x) => x * x;
console.log(square(5)); // Outputs: 25
```

### 3. **Callbacks**:

A callback is a function passed as an argument to another function. This technique allows a function to call another function.

Callback functions in JavaScript are used to handle asynchronous tasks and events. They are passed as arguments to functions and executed later. Common use cases include managing asynchronous operations, event handling, iterating over arrays, and working with Promises and async/await. Callbacks allow for responsive and event-driven programming in JavaScript.

```javascript
function processArray(arr, callback) {
  const result = [];
  for (let item of arr) {
    result.push(callback(item));
  }
  return result;
}

const numbers = [1, 2, 3, 4];
const squares = processArray(numbers, (x) => x * x);
console.log(squares); // Outputs: [1, 4, 9, 16]
```

### 4. **Closures**:

A closure is a function that has access to the parent scope, even after the parent function has closed.

```javascript
function outerFunction() {
  let count = 0;
  return function innerFunction() {
    count++;
    return count;
  };
}

const counter = outerFunction();
console.log(counter()); // Outputs: 1
console.log(counter()); // Outputs: 2
```

### 5. **Hoisiting**:

Hoisting is a concept in JavaScript that can be a bit confusing for developers who are new to the language. It refers to how variable and function declarations are processed by the JavaScript engine during the compilation phase before the code is executed. Hoisting can lead to unexpected behavior in your code if you're not aware of how it works.

Here's a simplified explanation of hoisting in JavaScript:

1. **Variable Declarations**: When you declare a variable using the `var` keyword, JavaScript hoists the declaration to the top of the current function or global scope. This means that the variable declaration is moved to the top of its containing function or script block during the compilation phase, regardless of where in the code you actually wrote it.

   ```javascript
   console.log(myVar); // undefined
   var myVar = 10;
   console.log(myVar); // 10
   ```

   In the example above, `myVar` is hoisted, so the first `console.log` doesn't result in an error, but it prints `undefined`.

2. **Function Declarations**: Function declarations are also hoisted to the top of their containing scope. This means you can call a function before it's defined in your code.

   ```javascript
   sayHello(); // "Hello, World!"
   function sayHello() {
     console.log("Hello, World!");
   }
   ```

   In this case, `sayHello` is hoisted, so you can call it before the actual declaration.

However, there are some nuances to hoisting that you should be aware of:

- **Variable Initialization**: While variable declarations are hoisted, their assignments or initializations are not. So, in the example above, `myVar` was hoisted, but its value was assigned later in the code.

- **Block Scoping (let and const)**: Variables declared with `let` and `const` are also hoisted, but they are not initialized until the actual code execution reaches their declaration in the block. This is known as the "temporal dead zone." Trying to access such variables before their declaration results in a `ReferenceError`.

  ```javascript
  console.log(myVar); // ReferenceError
  let myVar = 10;
  ```

In summary, hoisting is a JavaScript behavior where variable and function declarations are moved to the top of their containing scope during compilation. Understanding how hoisting works can help you avoid unexpected behavior in your code and write more maintainable JavaScript. It's essential to declare your variables and functions in a way that aligns with your intended use to avoid confusion.

### 6. **IIFE (Immediately Invoked Function Expressions)**:

An IIFE is a function that runs as soon as it is defined.

```javascript
(function () {
  console.log("This will run immediately!");
})();
```

### 7. **Recursion**:

Recursion is a technique where a function calls itself.

```javascript
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

console.log(factorial(5)); // Outputs: 120
```

In the above example, the `factorial` function calls itself multiple times, decrementing the value of `n` until it reaches 1.

---

## Objects & Arrays

### 1. **Object Literals**:

An object literal is a list of zero or more pairs of property names and associated values, enclosed in curly braces (`{}`).

```javascript
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 30,
  greet: function () {
    return "Hello, " + this.firstName;
  },
};

console.log(person.greet()); // Outputs: Hello, John
```

### 2. **Constructors**:

Constructors are functions used to create and initialize objects. They are typically capitalized to differentiate them from regular functions.

```javascript
function Car(make, model) {
  this.make = make;
  this.model = model;
  this.drive = function () {
    return "Vroom!";
  };
}

const myCar = new Car("Toyota", "Corolla");
console.log(myCar.drive()); // Outputs: Vroom!
```

### 3. **Prototypes & Inheritance**:

Every object in JavaScript has a prototype from which it inherits properties. You can add properties to an object's prototype, making them available to all instances of that object.

```javascript
function Dog(name) {
  this.name = name;
}

Dog.prototype.bark = function () {
  return this.name + " says woof!";
};

const dog1 = new Dog("Buddy");
console.log(dog1.bark()); // Outputs: Buddy says woof!
```

Inheritance allows one object type to inherit properties and methods from another.

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.eat = function () {
  return this.name + " eats.";
};

function Bird(name) {
  Animal.call(this, name);
}

Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.fly = function () {
  return this.name + " flies.";
};

const bird1 = new Bird("Sparrow");
console.log(bird1.eat()); // Outputs: Sparrow eats.
console.log(bird1.fly()); // Outputs: Sparrow flies.
```

### 4. **ES6 Classes & Subclasses**:

ES6 introduced a `class` syntax to create objects and handle inheritance, providing a cleaner and more intuitive way to work with object-oriented programming in JavaScript.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  eat() {
    return `${this.name} eats.`;
  }
}

class Bird extends Animal {
  fly() {
    return `${this.name} flies.`;
  }
}

const eagle = new Bird("Eagle");
console.log(eagle.eat()); // Outputs: Eagle eats.
console.log(eagle.fly()); // Outputs: Eagle flies.
```

### 5. **Arrays & Array Methods**:

Arrays are ordered collections of items. Each item in an array has an index, starting from 0.

```javascript
const fruits = ["apple", "banana", "cherry"];

// Adding to the end of an array
fruits.push("date");

// Removing from the end of an array
fruits.pop();

// Adding to the beginning of an array
fruits.unshift("avocado");

// Removing from the beginning of an array
fruits.shift();

// Finding the index of an item
const index = fruits.indexOf("banana");

// Removing an item by index position
fruits.splice(index, 1);
```

### 6. **Destructuring**:

Destructuring allows you to unpack values from arrays or properties from objects into distinct variables.

- **Array Destructuring**:

```javascript
const colors = ["red", "green", "blue"];
const [firstColor, secondColor] = colors;
console.log(firstColor); // Outputs: red
console.log(secondColor); // Outputs: green
```

- **Object Destructuring**:

```javascript
const person = {
  name: "Alice",
  age: 28,
};

const { name, age } = person;
console.log(name); // Outputs: Alice
console.log(age); // Outputs: 28
```

---

## Advanced Concepts

### 1. **Promises & Async/Await**:

- **Promises**: A Promise represents a value that might not be available yet. It's an object that has three states: pending, resolved (fulfilled), or rejected.

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Data fetched!");
    // reject("Error fetching data");
  }, 2000);
});

promise.then((data) => console.log(data)).catch((error) => console.log(error));
```

- **Async/Await**: A syntactic feature introduced in ES8 to work with promises in a more synchronous manner.

```javascript
async function fetchData() {
  let response = await fetch("https://api.example.com/data");
  let data = await response.json();
  console.log(data);
}

fetchData();
```

### 2. **Generators & Iterators**:

- **Generators**: Functions that can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances.

```javascript
function* idGenerator() {
  let id = 0;
  while (true) {
    yield id++;
  }
}

const generateId = idGenerator();
console.log(generateId.next().value); // Outputs: 0
console.log(generateId.next().value); // Outputs: 1
```

- **Iterators**: Objects that have a `next()` method which returns the next item in the sequence.

```javascript
const array = [1, 2, 3];
const iterator = array[Symbol.iterator]();

console.log(iterator.next()); // Outputs: { value: 1, done: false }
```

### 3. **The Event Loop & JS Architecture**:

JavaScript is single-threaded, meaning it can execute only one command at a time. However, it's able to handle many tasks being asynchronous, like when fetching data.

- **Call Stack**: Where JS functions are put to be executed.
- **Callback Queue**: Where callbacks wait to be executed after their corresponding functions finish.
- **Event Loop**: Checks if the call stack is empty. If it is, it takes the first event from the callback queue and pushes it to the call stack.

This architecture ensures that the browser remains responsive. Even if a task takes a long time (like fetching data), other operations like UI updates aren't blocked.

### 4. **Modules (CommonJS, ES6 Modules)**:

- **CommonJS**: Used mainly in Node.js. Modules are imported using `require` and exported using `module.exports`.

```javascript
// math.js
module.exports = {
  add: (a, b) => a + b,
};

// app.js
const math = require("./math");
console.log(math.add(2, 3)); // Outputs: 5
```

- **ES6 Modules**: Used in modern browsers and frontend frameworks. Use `import` and `export` statements.

```javascript
// math.js
export const add = (a, b) => a + b;

// app.js
import { add } from "./math.js";
console.log(add(2, 3)); // Outputs: 5
```

### 5. **Error Handling (try, catch, finally)**:

Allows you to handle runtime errors gracefully.

```javascript
try {
  // Potentially error-causing code
  console.log(variableThatDoesNotExist);
} catch (error) {
  console.log("An error occurred:", error.message);
} finally {
  console.log("This always runs, error or not.");
}
```

### 6. **Regular Expressions**:

Patterns used to match character combinations in strings.

```javascript
const regex = /hello/i; // i makes it case-insensitive
const str = "Hello world";
console.log(regex.test(str)); // Outputs: true
```

---

The event loop, in particular, is a fundamental concept to grasp in JavaScript. It's the heart of the non-blocking, asynchronous behavior in the language, allowing for efficient execution even when tasks are IO-bound or particularly heavy.
