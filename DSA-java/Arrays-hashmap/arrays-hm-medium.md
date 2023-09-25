---

### 1. Group Anagrams

**Question**: Given an array of strings, group anagrams together. An anagram is when you can rearrange the characters of one word to form another word.

**Approach**: The key insight is that anagrams will always have the same characters when sorted. We can sort each string and use the sorted version as a key in a hashmap. The corresponding value will be a list of all strings that, when sorted, match that key.

- Time Complexity: O(n * klogk) where `n` is the number of strings and `k` is the average length of a string.
- Space Complexity: O(nk)

**Java Code**:
```java
public List<List<String>> groupAnagrams(String[] strs) {
    if (strs.length == 0) return new ArrayList<>();

    Map<String, List<String>> map = new HashMap<>();

    for (String s : strs) {
        char[] ca = s.toCharArray();
        Arrays.sort(ca);
        String key = String.valueOf(ca);
        if (!map.containsKey(key)) map.put(key, new ArrayList<>());
        map.get(key).add(s);
    }

    return new ArrayList<>(map.values());
}
```

---

### 2. Subarray Sum Equals K

**Question**: Given an array of integers and an integer `k`, you need to find the total number of continuous subarrays whose sum equals `k`.

**Approach**: Use a hashmap to store the cumulative sum up to each index. For each cumulative sum, calculate `sum - k` and see how many times this value has occurred before. This will give the number of subarrays ending at the current index that have a sum of `k`.

- Time Complexity: O(n)
- Space Complexity: O(n)

**Java Code**:

```java
public int subarraySum(int[] nums, int k) {
    int count = 0, sum = 0;
    HashMap<Integer, Integer> preSum = new HashMap<>();
    preSum.put(0, 1);

    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (preSum.containsKey(sum - k)) {
            count += preSum.get(sum - k);
        }
        preSum.put(sum, preSum.getOrDefault(sum, 0) + 1);
    }
    return count;
}
```

Explanation:
we search for sum - k in the map, if it exists, it means that there is a subarray that sums up to k. We also update the prefix sum in the map. The key is the prefix sum and the value is the number of occurrences of the prefix sum.

```
.............sum
.....sum-k.....k

sum - (sum - k) = k
```

> similarly to find the sub array sum equal to 0, we can use the same approach by replacing k with 0. searching for sum - 0 = sum in the map.

---

### 3. Top K Frequent Elements

**Question**: Given a non-empty array of integers, return the `k` most frequent elements.

**Approach**: Use a hashmap to store the frequency of each number. Then, sort the numbers based on their frequencies to get the top k frequent numbers.

- Time Complexity: O(nlogn)
- Space Complexity: O(n)

**Java Code**:

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> frequency = new HashMap<>();
    for (int num : nums) {
        frequency.put(num, frequency.getOrDefault(num, 0) + 1);
    }

    List<Integer> uniqueNumbers = new ArrayList<>(frequency.keySet());
    Collections.sort(uniqueNumbers, (a, b) -> frequency.get(b).compareTo(frequency.get(a)));

    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
        result[i] = uniqueNumbers.get(i);
    }
    return result;
}
```

> Note: We can also use a min heap to get the top k frequent elements in O(nlogk) time.

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> frequency = new HashMap<>();
    for (int num : nums) {
        frequency.put(num, frequency.getOrDefault(num, 0) + 1);
    }

    PriorityQueue<Integer> heap = new PriorityQueue<>((a, b) -> frequency.get(a) - frequency.get(b));

    for (int num : frequency.keySet()) {
        heap.add(num);
        if (heap.size() > k) heap.poll();
    }

    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
        result[i] = heap.poll();
    }
    return result;
}

```

---

### 4. Longest Substring Without Repeating Characters

**Question**: Given a string, find the length of the longest substring without repeating characters.

**Approach**: Use a sliding window approach. Keep expanding the right end of the window as long as there's no repetition. If a repetition is found, increment the left end of the window.

- Time Complexity: O(n)
- Space Complexity: O(min(m, n)) where n is the size of the string and m is the character set.

**Java Code**:

```java
public int lengthOfLongestSubstring(String s) {
    int n = s.length();
    Set<Character> set = new HashSet<>();
    int ans = 0, i = 0, j = 0;

    while (i < n && j < n) {
        if (!set.contains(s.charAt(j))) {
            set.add(s.charAt(j++));
            ans = Math.max(ans, j - i);
        } else { //
            set.remove(s.charAt(i++));
        }
    }
    return ans;
}
```

---

### 5. Number of Islands

**Question**: Given a 2D grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

**Approach**: Perform a Depth First Search (DFS) whenever you encounter a '1'. Every visited cell will be marked as '0' to avoid counting it again.

- Time Complexity: O(m \* n) where m and n are the dimensions of the grid.
- Space Complexity: O(m \* n)

**Java Code**:

```java
public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) return 0;

    int count = 0;
    for (int i = 0; i < grid.length; i++) {
        for (int j = 0; j < grid[0].length; j++) {
            if (grid[i][j] == '1') {
                DFS(grid, i, j);
                count++;
            }
        }
    }
    return count;
}

private void DFS(char[][] grid, int i, int j) {
    if (i < 0 || i >= grid.length || j < 0 || j >= grid

[0].length || grid[i][j] == '0') return;

    grid[i][j] = '0'; // Marking the cell as visited
    DFS(grid, i+1, j);
    DFS(grid, i-1, j);
    DFS(grid, i, j+1);
    DFS(grid, i, j-1);
}
```

---
