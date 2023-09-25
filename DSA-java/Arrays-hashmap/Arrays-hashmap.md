Arrays and HashMaps (often referred to as hash tables) are fundamental data structures that are frequently used to solve a plethora of problems in computer science and software development. Here's an in-depth explanation of both:

## Arrays

### What are Arrays?

Arrays are contiguous memory locations that store multiple items of the same type. Each item can be accessed via its index.

### Basic Operations on Arrays:

1. **Insertion**: Add an element at the end or at any given position.
2. **Deletion**: Remove an element from a particular position.
3. **Traversal**: Access each element.

### Common Techniques to Solve Array Problems:

1. **Iteration**: Simply loop through elements of an array.
2. **2-Pointer Technique**: Use two pointers to solve problems, particularly useful for sorted arrays.
3. **Sliding Window**: Useful to calculate something "on the fly" as we move through the array.
4. **Prefix Sum**: For quick range sum queries.
5. **Binary Search**: For searching in sorted arrays.

**Examples**:

1. **Iteration**:

> When you need to access each element in an array.

Find the maximum element in an array.

```java
public int findMax(int[] arr) {
    int max = Integer.MIN_VALUE;
    for (int num : arr) { // for (int i = 0; i < arr.length; i++)
        max = Math.max(max, num);
    }
    return max;
}
```

2. **2-Pointer Technique**:

> When the array is sorted or when you need to search for a pair of numbers that meet a certain condition.

Find if there are pairs in a sorted array that sum up to a target.

```java
public boolean hasPairWithSum(int[] arr, int sum) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        if (arr[left] + arr[right] == sum) return true;
        if (arr[left] + arr[right] < sum) left++;
        else right--;
    }
    return false;
}
```

3. **Sliding Window**:

> When you need to find a subarray that satisfies certain conditions without checking all possible subarrays.

Find the maximum sum of a subarray of size k.

```java
public int maxSumOfSubarrayOfSizeK(int[] arr, int k) {
    int maxSum = 0, windowSum = 0, windowStart = 0;
    for (int windowEnd = 0; windowEnd < arr.length; windowEnd++) {
        windowSum += arr[windowEnd];
        if (windowEnd >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);
            windowSum -= arr[windowStart];
            windowStart++;
        }
    }
    return maxSum;
}
```

## Hashmap

### What is a HashMap?

A HashMap is a data structure that uses a hash function to map identifying values (keys) to their associated values.

### Basic Operations on HashMap:

1. **Insertion**: Add a key-value pair.
2. **Deletion**: Remove a key-value pair using a key.
3. **Lookup**: Fetch a value using a key.

### Common Techniques to Solve HashMap Problems:

1. **Frequency Count**: Using the HashMap to count occurrences.
2. **Grouping**: Group by properties.
3. **Prefix Sum with HashMap**: Useful in subarray problems.

**Examples**:

1. **Frequency Count**:

> When you need to count the number of occurrences of something.

Find the first non-repeating character in a string.

```java
public int findFirstNonRepeatingCharacter(String s) {
    HashMap<Character, Integer> frequencyMap = new HashMap<>();
    for (char c : s.toCharArray()) {
        frequencyMap.put(c, frequencyMap.getOrDefault(c, 0) + 1);
    }
    for (int i = 0; i < s.length(); i++) {
        if (frequencyMap.get(s.charAt(i)) == 1) return i;
    }
    return -1;
}
```

2. **Prefix Sum with HashMap**:

> When you need to calculate the sum of a range of values.

Find the number of subarrays that sum up to a target.

```java
public int subarraySumEqualsK(int[] nums, int k) {
    int count = 0, sum = 0;
    HashMap<Integer, Integer> preSum = new HashMap<>();
    preSum.put(0, 1);
    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (preSum.containsKey(sum - k)) {
            count += preSum.get(sum - k);
        }
        preSum.put(sum, preSum.getOrDefault(sum, 0) + 1); // update prefix sum, if already exists, increment by 1 else put 1
    }
    return count;
}
```

Explanation:
we search for sum - k in the map, if it exists, it means that there is a subarray that sums up to k. We also update the prefix sum in the map. The key is the prefix sum and the value is the number of occurrences of the prefix sum.

```
............sum
.....sum-k.....k

sum - (sum - k) = k
```

## Conclusion

Both arrays and HashMaps are incredibly versatile. Learning to recognize when to apply these structures and techniques is key to solving a wide range of algorithmic problems.
