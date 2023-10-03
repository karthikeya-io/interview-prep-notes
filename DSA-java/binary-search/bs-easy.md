### 1. Search Insert Position

**Question**:
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

**Approach**:
Binary search. If the target is found, return its index. If not found, the `left` pointer will indicate the position where it should be inserted.

```java
public int searchInsert(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;  // To avoid potential overflow

        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return left;  // The desired position if not found
}
```

**Explanation**:
The binary search looks for the target. If not found, due to the nature of binary search, `left` will point to the position where the target should be inserted.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### 2. Guess Number Higher or Lower

**Question**:
We're playing the Guess Game. The game picks a number from 1 to `n`. You need to guess which number game picked. There's a predefined function `guess(int num)` which returns:

- `-1` if my number is lower,
- `1` if my number is higher,
- `0` if my number is equal.

**Approach**:
Binary search between 1 to n. Use the `guess` function to determine where the target is.

```java
public int guessNumber(int n) {
    int left = 1, right = n;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        int result = guess(mid);

        if (result == 0) {
            return mid;
        } else if (result == 1) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;  // This should never happen as the number is always between 1 to n
}
```

**Explanation**:
Just like a standard binary search but instead of comparing with a target directly, we use the `guess` function to get a hint.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### 3. First Bad Version

**Question**:
You're given an API `isBadVersion(version)` which tells whether a version is bad. Implement a function to find the first bad version.

**Approach**:
Binary search. Instead of comparing to a specific target value, we'll use the `isBadVersion` function.

```java
public int firstBadVersion(int n) {
    int left = 1, right = n;

    while (left < right) { // Notice the condition here
        int mid = left + (right - left) / 2;

        if (isBadVersion(mid)) {
            right = mid;  // Move left to find the first occurrence
        } else {
            left = mid + 1;
        }
    }

    return left;  // The first bad version
}
```

**Explanation**:
This binary search looks for the first occurrence where `isBadVersion` is true.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### Note:

For these easy problems, binary search provides a very efficient solution. In some cases, a linear search can be done, but it would be less efficient (O(n)) than the binary search (O(log n)).

### 4. Square Root of an Integer

**Question**:
Given a non-negative integer `x`, compute and return the square root of `x`. Only the integer part of the result is returned. (For example, if the answer is 2.8, return 2)

**Approach**:
Binary search between 0 and x. If mid \* mid is equal to x, return mid. If it's less, then the result must lie on the right side of mid, else on the left side.

```java
public int mySqrt(int x) {
    if (x == 0 || x == 1) return x;

    int left = 0, right = x;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // If mid*mid is the number, return mid
        if (mid == x / mid) { // Using division to avoid overflow
            return mid;
        }
        if (mid < x / mid) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    // Since we're looking for the integer part, return right
    return right;
}
```

**Explanation**:
The key insight is that the square root of any number in the range [0, x] will not exceed x. Using this range, we perform binary search.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### 5. Valid Perfect Square

**Question**:
Given a positive integer `num`, write a function that returns `true` if `num` is a perfect square else `false`.

**Approach**:
Similar to the previous problem, but here we are checking for the exact square.

```java
public boolean isPerfectSquare(int num) {
    if (num < 2) return true;

    long left = 2, right = num / 2; // Using long to avoid potential overflows

    while (left <= right) {
        long mid = left + (right - left) / 2;
        long squared = mid * mid;

        if (squared == num) {
            return true;
        }

        if (squared < num) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return false;
}
```

**Explanation**:
The primary logic is to perform a binary search on the number. If at any point our mid \* mid equals the number, then it's a perfect square. Else, if we exit the loop without finding such a number, it's not a perfect square.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### Note:

last 2 problems are essentially evaluating the nature of numbers with respect to their squares. The binary search is highly efficient for these kinds of problems. Although one could potentially check every number sequentially to see if its square is the target, this would be much slower and lead to a time complexity of O(n).
