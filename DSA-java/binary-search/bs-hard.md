## Binary Search - Hard

### 1. Median of Two Sorted Arrays

**Question**:
Given two sorted arrays, find the median.

**Example**:

```
nums1 = [1, 3]
nums2 = [2]
Output: 2.0
```

**Simple Explanation**:
Imagine we cut both arrays at some positions, so the numbers on the left of both arrays combined are half the total numbers (or half + 1 if the total count is odd). Now, the median is just the biggest number on the left if the total count is odd, or the average of the biggest on the left and the smallest on the right if it's even.

**Solution**:

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    // Always keep nums1 as the shorter array
    if (nums1.length > nums2.length) {
        return findMedianSortedArrays(nums2, nums1);
    }

    int x = nums1.length;
    int y = nums2.length;
    int low = 0, high = x;

    while (low <= high) {
        int partitionX = (low + high) / 2; // Cut position in nums1
        int partitionY = (x + y + 1) / 2 - partitionX; // Corresponding cut position in nums2

        // Edge elements after cutting nums1 and nums2
        int maxX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
        int minX = (partitionX == x) ? Integer.MAX_VALUE : nums1[partitionX];

        int maxY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
        int minY = (partitionY == y) ? Integer.MAX_VALUE : nums2[partitionY];

        // The correct cut is found
        if (maxX <= minY && maxY <= minX) {
            if ((x + y) % 2 == 0) {
                return ((double) Math.max(maxX, maxY) + Math.min(minX, minY)) / 2;
            } else {
                return (double) Math.max(maxX, maxY);
            }
        } else if (maxX > minY) {
            high = partitionX - 1; // Move left in nums1
        } else {
            low = partitionX + 1; // Move right in nums1
        }
    }
    throw new IllegalArgumentException("Input arrays are not sorted.");
}
```

**Time Complexity**:
O(log(min(m, n)))

**Space Complexity**:
O(1)

### 2. Find Minimum in Rotated Sorted Array II

**Question**:
An array was sorted, but then it was rotated (some numbers taken from the start and put to the end). It may have duplicates. Find the minimum element.

**Example**:

```
nums = [2,2,2,0,1]
Output: 0
```

**Simple Explanation**:
Even if it's rotated, in a half of the array, numbers will remain sorted. If the middle number is bigger than the end number, the minimum is in the right half. If the middle is smaller, the minimum is in the left half. If the middle is the same as the end, we can't be sure, so we just check one less number.

**Solution**:

```java
public int findMin(int[] nums) {
    int low = 0, high = nums.length - 1;
    while (low < high) {
        int mid = (low + high) / 2;
        if (nums[mid] > nums[high]) {
            low = mid + 1; // Minimum is in right half
        } else if (nums[mid] < nums[high]) {
            high = mid;   // Minimum is in left half
        } else { // nums[mid] == nums[high]
            high--;       // Reduce search space by 1
        }
    }
    return nums[low];
}
```

**Time Complexity**:
O(log n) (best case) or O(n) (worst case when there are many duplicates)

**Space Complexity**:
O(1)

### 3. Kth Smallest Element in a Sorted Matrix

**Question**:
You have a matrix (2D array) where each row and each column are sorted. Find the kth smallest number in it.

**Example**:

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8
Output: 13
```

**Simple Explanation**:
The smallest number is in the top-left and the biggest in the bottom-right. We can guess a number in the middle and see how many numbers are smaller than it to figure out if our guess was too high or too low.

**Solution**:

```java
public int kthSmallest(int[][] matrix, int k) {
    int n = matrix.length;
    int low = matrix[0][0], high = matrix[n - 1][n - 1];

    while (low < high) {
        int mid = (low + high) / 2;
        int count = countLessThanEqual(matrix, mid);
        if (count < k) {
            low = mid + 1;
        } else {
            high = mid;
        }
    }
    return low;
}

// Counts how many numbers in matrix are smaller or

 equal to target
private int countLessThanEqual(int[][] matrix, int target) {
    int n = matrix.length;
    int count = 0;
    int row = 0, col = n - 1;

    while (row < n && col >= 0) {
        if (matrix[row][col] <= target) {
            count += col + 1;
            row++;
        } else {
            col--;
        }
    }
    return count;
}
```

**Time Complexity**:
O(n \* log(max-min)), where max and min are the biggest and smallest numbers in the matrix.

**Space Complexity**:
O(1)

### 4. Split Array Largest Sum

**Question**:
You have an array of numbers and you need to split them into "m" non-empty continuous subarrays. You want to minimize the largest sum of these subarrays. What's the smallest possible largest sum?

**Example**:

```
nums = [7,2,5,10,8]
m = 2
Output: 18
(There are different ways to split such as [7,2,5] and [10,8] but the one with the smallest maximum sum is [7,2,5,10] and [8])
```

**Simple Explanation**:
The answer is somewhere between the largest number and the sum of all numbers. We can guess a sum and see how many pieces we can split the array into. If we can split into more pieces, our guess was too low. If not, our guess was too high.

**Solution**:

```java
public int splitArray(int[] nums, int m) {
    long l = 0;
    long r = 0;
    for (int num : nums) {
        r += num;
        if (l < num) {
            l = num;
        }
    }
    long ans = r;
    while (l <= r) {
        long mid = (l + r) >> 1;
        if (isValid(nums, mid, m)) {
            ans = mid;
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }
    return (int)ans;
}

// Checks if it's possible to split nums into <= m subarrays such that each subarray's sum <= target
private boolean isValid(int[] nums, long target, int m) {
    int count = 1;
    long total = 0;
    for (int num : nums) {
        total += num;
        if (total > target) {
            total = num;
            count++;
            if (count > m) {
                return false;
            }
        }
    }
    return true;
}
```

**Time Complexity**:
O(n \* log(sum of array))

**Space Complexity**:
O(1)

### 5. Find the Duplicate Number

**Question**:
In an array of "n+1" numbers from 1 to n, one number is repeated. Find it.

**Example**:

```
nums = [3,1,3,4,2]
Output: 3
```

**Simple Explanation**:
Think of the numbers as pointing to an index. This repeated number creates a loop. Like runners on a track, if two runners start at different points but one is twice as fast, they'll eventually land on the same spot. Using this, we can find where the loop starts, which is our duplicate number.

**Solution**:

```java
public int findDuplicate(int[] nums) {
    // Find the intersection point of the two runners
    int tortoise = nums[0];
    int hare = nums[nums[0]];
    while (tortoise != hare) {
        tortoise = nums[tortoise];
        hare = nums[nums[hare]];
    }

    // Find the entrance to the loop (start of the cycle)
    hare = 0;
    while (tortoise != hare) {
        tortoise = nums[tortoise];
        hare = nums[hare];
    }

    return hare;
}
```

**Time Complexity**:
O(n)

**Space Complexity**:
O(1)
