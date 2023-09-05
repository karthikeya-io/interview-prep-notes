## Recursion

### 1. Introduction to Recursion

**Definition and Concept**:
Recursion is a method where the solution to a problem depends on solutions to smaller instances of the same problem. In programming, recursion happens when a function calls itself.

**Real-world Analogies**:

- **Russian Dolls**: Open one doll to find another one inside, then another inside that one, and so on. Each level is similar to a recursive call.
- **Mirror Reflection**: Imagine two mirrors facing each other. The reflection created is an infinite series of images of the mirror. This infinite nesting is analogous to recursion.

### 2. Fundamental Principles

**Base Case**:
This is the condition under which the recursion stops. Think of it as an 'exit condition'. Without this, the recursion could go on indefinitely.

**Recursive Case**:
This is where the function calls itself, typically with a modified argument.

**The Call Stack**:
Each time a function is called (including recursively), an entry (often called a frame) is added to the call stack. When the function exits, its frame is removed. If the call stack gets too deep (i.e., too many frames), a stack overflow occurs.

```
Call stack for `factorial(3)`:
|                  |
|------------------|
| factorial(1)     | <- Base case: Returns and pops off the stack.
|------------------|
| factorial(2)     |
|------------------|
| factorial(3)     | <- Starts here.
|------------------|
```

### 3. Basic Recursive Patterns

**Linear Recursion**:
A single recursive call per function.
Example: Computing factorial of a number.

```
factorial(3) = 3 * factorial(2)
factorial(2) = 2 * factorial(1)
factorial(1) = 1  # base case
```

**Binary (or Multiple) Recursion**:
Multiple recursive calls in a function.
Example: Fibonacci sequence.

```
fib(4) = fib(3) + fib(2)
fib(3) = fib(2) + fib(1)
fib(2) = 1
fib(1) = 1
```

**Tail Recursion**:
The recursive call is the last operation in the function. Some languages or compilers can optimize tail recursion. By optimizing, the compiler can avoid adding a new stack frame for the recursive call. This optimization is called tail call elimination. Which reduces the auxiliary space used during recursion.

```
def tail_factorial(n, accumulator=1):
    if n == 1:
        return accumulator
    else:
        return tail_factorial(n-1, n * accumulator)
```

### 4. Visualization and Understanding

**Flow of Recursive Calls**:
Visualize how a function progresses. For factorial:

```
factorial(3)
   |
   --> factorial(2)
          |
          --> factorial(1)
              |
              returns 1
          returns 2
   returns 6
```

**Tools for Visualization**:

- **Python Tutor**: Web-based tool that allows you to visualize Python code execution.
- **Hand-tracing**: Physically drawing out the call stack on paper as you work through the recursion.

### 5. Calculating Time Complexity of Recursive Functions

ToDo: update to make it clear

Sure! Analyzing the time complexity of recursive algorithms can initially seem daunting, but with techniques like the recurrence relation, recursion tree, and the master theorem, it becomes more manageable.

Let's explore three examples to showcase these methods:

1. **Factorial Function**

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n-1)
```

**Method: Recurrence Relation**
For \( n \) - \( T(n) \) represents the time taken.
\[ T(n) = T(n-1) + c \]
\[ T(n-1) = T(n-2) + c \]
\[ ... \]
\[ T(1) = c \]

When you sum these up, you get the series \( c + c + c + ... + c \) (n times), which is \( O(n) \).

2. **Binary Search**

```python
def binary_search(arr, low, high, x):
    if high >= low:
        mid = (high + low) // 2
        if arr[mid] == x:
            return mid
        elif arr[mid] > x:
            return binary_search(arr, low, mid - 1, x)
        else:
            return binary_search(arr, mid + 1, high, x)
    else:
        return -1
```

**Method: Recursion Tree**
Each node in the recursion tree represents a recursive call. At each level, the problem is halved. If the tree height is \( h \), then the total calls are \( 2^0 + 2^1 + ... + 2^h \), but since the problem is halved at each level, the depth of the tree is \( log(n) \). Thus, time complexity is \( O(log(n)) \).

3. **Merge Sort**

```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        L = arr[:mid]
        R = arr[mid:]

        merge_sort(L)
        merge_sort(R)

        # merge step, which runs in linear time O(n)
        i = j = k = 0
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1
        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1
        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
```

**Method: Master Theorem**
Merge sort can be described by the recurrence:
\[ T(n) = 2T(n/2) + n \]

Using the Master Theorem:

- a = 2 (Number of subproblems)
- b = 2 (Factor by which problem size is reduced)
- f(n) = n (Work outside of the recursive calls)

Here, \( f(n) = Θ(n^{\log_b{a}}) \)

So, according to the Master Theorem, the time complexity of the merge sort is \( O(n \log n) \).

Analyzing recursive algorithms requires practice, especially when there are multiple recursive calls or when additional work is done outside of these calls. By using methods like the recursion tree, recurrence relations, and the master theorem, you can systematically determine the time complexity of recursive algorithms.
