### Binary Search:

Binary search is a search algorithm that finds the position of a target value within a sorted array or list. It works by repeatedly dividing in half the portion of the list that could contain the target value, and then comparing the target value to the middle element of that portion. The process continues until the target value is found or the remaining portion is empty.

**Time Complexity**: O(log n)

- Every step you're cutting the list/array in half, thus the logarithmic time complexity.

**Space Complexity**: O(1) for the iterative approach, as it uses a constant amount of space.

- O(log n) for the recursive approach, due to the call stack.

### Advantages:

1. **Efficiency**: Binary search is significantly faster than a linear search for large datasets, especially when they're sorted. As the size of the dataset increases, the efficiency advantage of binary search becomes more pronounced.

2. **Read-Only**: It only requires sequential read access, and does not require writing to the data structure. Thus, it works with read-only mediums like CDs, DVDs, etc.

3. **Predictable**: The worst-case performance, the best-case performance, and the average performance are all O(log n), making its performance more predictable than other algorithms.

### Example:

**Iterative Binary Search**:

```java
public int binarySearchIterative(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;  // target not found
}
```

**Recursive Binary Search**:

```java
public int binarySearchRecursive(int[] nums, int target) {
    return binarySearchHelper(nums, target, 0, nums.length - 1);
}

private int binarySearchHelper(int[] nums, int target, int left, int right) {
    if (left > right) {
        return -1;  // target not found
    }

    int mid = left + (right - left) / 2;

    if (nums[mid] == target) {
        return mid;
    } else if (nums[mid] < target) {
        return binarySearchHelper(nums, target, mid + 1, right);
    } else {
        return binarySearchHelper(nums, target, left, mid - 1);
    }
}
```

Remember:

1. The recursive version has the overhead of function calls, which takes up space on the call stack.
2. The formula `mid = left + (right - left) / 2` is used to calculate the midpoint to avoid potential overflow with `mid = (left + right) / 2` when `left` and `right` are large numbers.
