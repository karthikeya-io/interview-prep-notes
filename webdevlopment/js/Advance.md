## 4. **Advanced JavaScript**:

### 1. **Functional Programming Concepts**:

Functional programming (FP) is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing state and mutable data. In FP, functions are first-class citizens, meaning they can be passed around and used as arguments or returned as values.

### 2. **Map, Reduce, Filter**:

These are higher-order functions that operate on arrays and are staples in functional programming.

- **Map**: Transforms an array by applying a function to all of its elements and building a new array from the returned values.

```javascript
const numbers = [1, 2, 3, 4];
const squared = numbers.map((x) => x * x);
console.log(squared); // Outputs: [1, 4, 9, 16]
```

> **Note**: The original array is not mutated. Different between `map` and `forEach` is that `map` returns a new array while `forEach` doesn't.

- **Reduce**: Takes an array and reduces its elements to a single value using a reducer function and an initial value.

```javascript
const sum = numbers.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  0
);
console.log(sum); // Outputs: 10
```

- **Filter**: Creates a new array with all elements that pass the test implemented by the provided function.

```javascript
const evenNumbers = numbers.filter((x) => x % 2 === 0);
console.log(evenNumbers); // Outputs: [2, 4]
```

### 3. **Pure Functions**:

A pure function is a function where the output value is determined only by its input values, without observable side effects. This means:

- For the same input, it will always produce the same output.
- It doesn't rely on or modify the external state (no side effects).

```javascript
function pureAdd(a, b) {
  return a + b;
}
```

Contrast this with an impure function:

```javascript
let value = 10;

function impureAdd(a) {
  return a + value; // Relies on external state
}
```

Pure functions are easier to reason about, test, and debug because they don't have hidden inputs or outputs.

### 4. **First-Class Functions**:

In JavaScript, functions are first-class citizens. This means that functions can:

- Be assigned to a variable.
- Be passed as an argument to another function.
- Return from another function.

```javascript
// Assigned to a variable
const greet = function () {
  return "Hello!";
};

// Passed as an argument
function runFunction(fn) {
  return fn();
}

console.log(runFunction(greet)); // Outputs: Hello!

// Return from another function
function multiplier(factor) {
  return function (x) {
    return x * factor;
  };
}

const double = multiplier(2);
console.log(double(5)); // Outputs: 10
```

### 5. **Higher-Order Functions**:

A higher-order function is a function that:

- Takes one or more functions as arguments.
- Returns a function as its result.

The `.map()`, `.reduce()`, and `.filter()` methods we discussed earlier are examples of higher-order functions. They take a function as an argument and use it to process the array.

Another example:

```javascript
function greaterThan(n) {
  return function (m) {
    return m > n;
  };
}

const greaterThan10 = greaterThan(10);
console.log(greaterThan10(15)); // Outputs: true
```

In the above example, `greaterThan` is a higher-order function that returns a function.

---

Understanding these advanced concepts is crucial for writing efficient, concise, and maintainable JavaScript code, especially as applications grow in complexity. They also form the foundation for many modern JavaScript libraries and frameworks.
