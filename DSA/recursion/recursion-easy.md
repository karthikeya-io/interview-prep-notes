## Recursion (Easy)

### 1. Factorial Calculation

**Question**: Write a recursive method that calculates the factorial of a given number `n`.

**Hint**: Remember that `n! = n * (n-1)!` and `0! = 1`.

**Approach**:

- If `n` is 0, return 1.
- Otherwise, return `n * factorial(n-1)`.

**Solution**:

```java
public class Factorial {
    public static int factorial(int n) {
        if (n == 0) {
            return 1;
        }
        return n * factorial(n - 1);
    }

    public static void main(String[] args) {
        System.out.println(factorial(5)); // Expected output: 120
    }
}
```

**Time Complexity**: \(O(n)\), as the recursive function is called `n` times.

### 2. Sum of an Array

**Question**: Write a recursive method to find the sum of elements in an array.

**Hint**: The sum of an array is the sum of the first element and the sum of the remaining elements.

**Approach**:

- If the array is empty, return 0.
- Otherwise, return the first element plus the sum of the rest.

**Solution**:

```java
public class ArraySum {
    public static int sum(int[] arr, int n) {
        if (n <= 0) {
            return 0;
        }
        return sum(arr, n-1) + arr[n-1];
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        System.out.println(sum(arr, arr.length)); // Expected output: 15
    }
}
```

**Time Complexity**: \(O(n)\), as the recursive function is called `n` times.

### 3. Palindrome Check

**Question**: Write a recursive method to check if a given string is a palindrome.

**Hint**: A string is a palindrome if the first and last characters are the same and the substring (excluding the first and last characters) is also a palindrome.

**Approach**:

- Compare the first and last characters.
- If they are different, return false.
- Otherwise, check the palindrome property for the substring.

**Solution**:

```java
public class PalindromeCheck {
    public static boolean isPalindrome(String str, int start, int end) {
        if (start >= end) {
            return true;
        }
        if (str.charAt(start) != str.charAt(end)) {
            return false;
        }
        return isPalindrome(str, start + 1, end - 1);
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("radar", 0, 4)); // Expected output: true
        System.out.println(isPalindrome("hello", 0, 4)); // Expected output: false
    }
}
```

**Time Complexity**: \(O(n/2)\), which simplifies to \(O(n)\). In the worst case, the recursive function checks half the string.

### 4. Fibonacci Sequence

**Question**: Write a recursive method to calculate the `n-th` Fibonacci number.

**Hint**: The Fibonacci sequence starts with 0 and 1, and each subsequent number is the sum of the two preceding ones.

**Approach**:

- If `n` is 0 or 1, return `n`.
- Otherwise, return `fib(n-1) + fib(n-2)`.

**Solution**:

```java
public class Fibonacci {
    public static int fib(int n) {
        if (n <= 1) {
            return n;
        }
        return fib(n-1) + fib(n-2);
    }

    public static void main(String[] args) {
        System.out.println(fib(5)); // Expected output: 5
    }
}
```

**Time Complexity**: \(O(2^n)\). This is a naive recursive solution, and its time complexity is exponential due to repeated calculations.

For each of the "Easy" problems, the solutions provided are straightforward recursive implementations. It's worth noting that some of these problems, like the Fibonacci sequence, have more efficient solutions using dynamic programming or memoization, but the primary aim here is to focus on understanding recursion.
