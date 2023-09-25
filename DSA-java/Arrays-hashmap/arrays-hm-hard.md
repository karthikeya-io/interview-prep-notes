Of course! Here are the hard problems explained with their optimal solutions:

---

### 1. LRU Cache

**Question**: Design and implement an LRU (Least Recently Used) cache. It should support the following operations: `get` and `put`.

**Approach**: Use a hashmap for O(1) lookup times and a doubly-linked list for O(1) insertions and deletions. The hashmap will store keys and their corresponding nodes in the doubly-linked list.

**Java Code**:

```java
class LRUCache {

    class Node {
        int key, value;
        Node prev, next;

        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private Map<Integer, Node> map;
    private int capacity, count;
    private Node head, tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.count = 0;
        map = new HashMap<>();

        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        Node n = map.get(key);
        if(n == null) return -1; // cache miss
        update(n); // move the accessed item to the front
        return n.value;
    }

    public void put(int key, int value) {
        Node n = map.get(key);
        if(n == null) {
            n = new Node(key, value);
            map.put(key, n);
            add(n);
            count++;
            if(count > capacity) { // remove the oldest item if the capacity is full
                map.remove(tail.prev.key);
                remove(tail.prev);
                count--;
            }
        } else {
            n.value = value; // update the value
            update(n); // move the modified item to the front
        }
    }

    private void add(Node n) {
        Node after = head.next;
        head.next = n;
        n.prev = head;
        n.next = after;
        after.prev = n;
    }

    private void remove(Node n) {
        Node before = n.prev;
        Node after = n.next;
        before.next = after;
        after.prev = before;
    }

    private void update(Node n) {
        remove(n);
        add(n);
    }
}
```

---

### 2. Max Points on a Line

**Question**: Given an array of points, find the maximum number of points that lie on the same straight line.

**Approach**: For each point, calculate the slope with every other point and track the number of times each slope occurs using a hashmap.

**Java Code**:

```java
public int maxPoints(int[][] points) {
    if (points == null) return 0;
    if (points.length <= 2) return points.length;

    Map<Integer, Map<Integer, Integer>> map = new HashMap<>();
    int result = 0;
    for (int i = 0; i < points.length; i++) {
        map.clear();
        int overlap = 0, max = 0;
        for (int j = i + 1; j < points.length; j++) {
            int x = points[j][0] - points[i][0];
            int y = points[j][1] - points[i][1];
            if (x == 0 && y == 0) {
                overlap++;
                continue;
            }
            int gcd = generateGCD(x, y);
            if (gcd != 0) {
                x /= gcd;
                y /= gcd;
            }

            if (map.containsKey(x)) {
                if (map.get(x).containsKey(y)) {
                    map.get(x).put(y, map.get(x).get(y) + 1);
                } else {
                    map.get(x).put(y, 1);
                }
            } else {
                Map<Integer, Integer> m = new HashMap<>();
                m.put(y, 1);
                map.put(x, m);
            }
            max = Math.max(max, map.get(x).get(y));
        }
        result = Math.max(result, max + overlap + 1);
    }
    return result;
}

private int generateGCD(int a, int b) {
    if (b == 0) return a;
    else return generateGCD(b, a % b);
}
```

---

### 3. Minimum Window Substring

**Question**: Given a string S and a string T, find the minimum window in S which will contain all the characters in T.

**Approach**: Use the sliding window technique with two pointers. Expand the right end of the window until you've covered all characters in T, and then shrink the left end of the window to find the minimum.

**Java Code**:

```java
public String

 minWindow(String s, String t) {
    if (s.length() == 0 || t.length() == 0) return "";

    Map<Character, Integer> dictT = new HashMap<>();
    for (int i = 0; i < t.length(); i++) {
        char c = t.charAt(i);
        dictT.put(c, dictT.getOrDefault(c, 0) + 1);
    }

    int l = 0, r = 0, formed = 0, required = dictT.size();
    Map<Character, Integer> windowCounts = new HashMap<>();
    int[] ans = {-1, 0, 0};

    while (r < s.length()) {
        char c = s.charAt(r);
        windowCounts.put(c, windowCounts.getOrDefault(c, 0) + 1);
        if (dictT.containsKey(c) && windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
            formed++;
        }

        while (l <= r && formed == required) {
            c = s.charAt(l);
            if (ans[0] == -1 || r - l + 1 < ans[0]) {
                ans[0] = r - l + 1;
                ans[1] = l;
                ans[2] = r;
            }
            windowCounts.put(c, windowCounts.get(c) - 1);
            if (dictT.containsKey(c) && windowCounts.get(c).intValue() < dictT.get(c).intValue()) {
                formed--;
            }
            l++;
        }
        r++;
    }
    return ans[0] == -1 ? "" : s.substring(ans[1], ans[2] + 1);
}
```

---

### 4. Longest Consecutive Sequence

**Question**: Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

**Approach**: Use a hashmap to store each number in the array. For each number, check if it's the beginning of a sequence and then try to extend the sequence.

**Java Code**:

```java
public int longestConsecutive(int[] nums) {
    Set<Integer> numSet = new HashSet<>();
    for (int num : nums) {
        numSet.add(num);
    }

    int longestStreak = 0;

    for (int num : numSet) {
        if (!numSet.contains(num - 1)) {
            int currentNum = num;
            int currentStreak = 1;

            while (numSet.contains(currentNum + 1)) {
                currentNum += 1;
                currentStreak += 1;
            }

            longestStreak = Math.max(longestStreak, currentStreak);
        }
    }
    return longestStreak;
}
```

---

### 5. The Skyline Problem

**Question**: Given the positions and heights of buildings, compute the skyline formed by these buildings collectively.

**Approach**: Use a priority queue to track the height of the buildings. For each building, treat its start and end as separate events and sort all the events. Traverse through these events and update the queue.

**Java Code**:

```java
public List<List<Integer>> getSkyline(int[][] buildings) {
    List<List<Integer>> result = new ArrayList<>();
    List<int[]> height = new ArrayList<>();

    for (int[] b : buildings) {
        height.add(new int[]{b[0], -b[2]});
        height.add(new int[]{b[1], b[2]});
    }

    Collections.sort(height, (a, b) -> {
        if (a[0] != b[0]) return a[0] - b[0];
        return a[1] - b[1];
    });

    PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);
    pq.offer(0);
    int prev = 0;

    for (int[] h : height) {
        if (h[1] < 0) {
            pq.offer(-h[1]);
        } else {
            pq.remove(h[1]);
        }
        int curr = pq.peek();
        if (prev != curr) {
            result.add(Arrays.asList(h[0], curr));
            prev = curr;
        }
    }
    return result;
}
```

I've tried to break down each problem as simply as possible, using comments for better understanding. Let me know if you need further clarification on any problem!
