### 1. Find Peak Element

**Question**:
Given an array of integers `nums`, find the peak element. An element is considered as a peak if it is NOT smaller than its neighbors. You may imagine that `nums[-1] = nums[n] = -∞`. You must write an algorithm that runs in O(log n) time.

**Approach**:
Binary Search. If `nums[mid] < nums[mid + 1]`, then there is definitely a peak on the right side. Otherwise, a peak is on the left side.

```java
public int findPeakElement(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] < nums[mid + 1]) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return left;
}
```

**Explanation**:
By comparing the middle element with its right neighbor, we can decide which half of the array to search for the peak element.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### 2. Search in Rotated Sorted Array

**Question**:
Given an integer array `nums` sorted in ascending order, and an integer `target`. Suppose that `nums` is rotated at some pivot unknown to you beforehand (i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`). You should return the index of `target` in the array, or `-1` if `target` is not present in `nums`.

**Approach**:
Modified Binary Search. Check which half of the array is sorted after the rotation and decide the search space accordingly.

```java
public int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left <= right) {
        int mid = (left + right) / 2;

        if (nums[mid] == target) return mid;

        if (nums[left] <= nums[mid]) {
            // Left half is sorted
            if (target >= nums[left] && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else {
            // Right half is sorted
            if (target > nums[mid] && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }

    return -1;  // Target not found
}
```

**Explanation**:
This problem is a classic binary search problem but with a twist. The array is rotated, so we need to find out which part of the array is sorted and decide our search space accordingly.

**Complexities**:

- Time: O(log n)
- Space: O(1)

> If the array contains duplicates, the worst case is O(n) because we can't decide which half is sorted. For example, `[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1]` and `target = 0`. but the average case is still O(log n).

```java
public boolean search(int[] nums, int target) {
    int start = 0;
    int end = nums.length - 1;

    while (start <= end) {
        int mid = start + (end - start) / 2;

        if (nums[mid] == target) {
            return true;
        }

        // If we can't determine which half is sorted due to duplicates
        if (nums[start] == nums[mid]) {
            start++; // Skip the duplicate element
        }
        // Left half is sorted
        else if (nums[start] < nums[mid]) {
            if (target >= nums[start] && target < nums[mid]) {
                // Target is in the left half
                end = mid - 1;
            } else {
                // Target is in the right half
                start = mid + 1;
            }
        }
        // Right half is sorted
        else {
            if (target > nums[mid] && target <= nums[end]) {
                // Target is in the right half
                start = mid + 1;
            } else {
                // Target is in the left half
                end = mid - 1;
            }
        }
    }

    return false; // Target not found
}

```

### 3. Find Minimum in Rotated Sorted Array

**Question**:
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand. Find the minimum element. The array may contain duplicates.

**Approach**:
Binary Search. If middle element is greater than the last element, the minimum lies in the right half, else in the left half.

```java
public int findMin(int[] nums) {
    int left = 0, right = nums.length - 1;

    while (left < right) {
        int mid = (left + right) / 2;

        if (nums[mid] > nums[right]) {
            left = mid + 1;
        } else if (nums[mid] < nums[right]) {
            right = mid;
        } else {
            right--;
        }
    }

    return nums[left];
}
```

**Explanation**:
In a rotated sorted array, the minimum element is the pivot. Comparing the middle element with the last element, we decide which half to search.

**Complexities**:

- Time: O(log n) in the average case, O(n) in the worst case (when there are many duplicates)
- Space: O(1)

### Note:

These problems are variants of binary search and are optimal with the given approach. The trickiness comes from dealing with the rotated nature of the array and handling duplicates, which slightly alters the traditional binary search.

### 4. Find the Duplicate Number

**Question**:
Given an array `nums` containing `n + 1` integers where each integer is in the range [1, n] inclusive, prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one in O(1) space complexity and less than O(n^2) time complexity.

**Approach**:
Binary Search. Treat the numbers as indices and find a cycle in the linked list formed by these indices.

```java
public int findDuplicate(int[] nums) {
    int slow = nums[0];
    int fast = nums[0];

    // Finding the intersection point of the two runners
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);

    // Finding the entrance to the cycle
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }

    return fast;
}
```

**Explanation**:
This problem can be solved using the Floyd's Tortoise and Hare (Cycle Detection) algorithm. We are using the array's values as pointers to other indices and finding the cycle in the sequence.

**Complexities**:

- Time: O(n)
- Space: O(1)

### 5. Find First and Last Position of Element in Sorted Array

**Question**:
Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value. If the target is not found in the array, return `[-1, -1]`. You must write an algorithm with O(log n) runtime complexity.

**Approach**:
Binary Search. Perform binary search twice, once to find the starting position of the element and once to find the ending position.

```java
public int[] searchRange(int[] nums, int target) {
    int[] result = new int[]{-1, -1};

    // First binary search to find the starting position
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    if (left == nums.length || nums[left] != target) {
        return result;
    }

    result[0] = left;

    // Second binary search to find the ending position
    right = nums.length - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (nums[mid] <= target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    result[1] = right;

    return result;
}
```

**Explanation**:
We perform two binary searches. The first one is to find the leftmost (first occurring) target, and the second one is to find the rightmost (last occurring) target.

**Complexities**:

- Time: O(log n)
- Space: O(1)

### Note:

For both problems, binary search is the optimal approach, and no alternative method would give better efficiency for the given constraints. The trick in these problems is to carefully adjust the left and right pointers and correctly initialize them for each binary search.
